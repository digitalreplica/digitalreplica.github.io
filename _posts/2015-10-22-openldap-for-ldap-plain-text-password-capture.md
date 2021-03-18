---
title:  "OpenLDAP for LDAP Plain Text Password Capture"
categories: hacking
excerpt: "How to set up a malicious ldap server to capture credentials during a penetration test"
---
![OpenLDAP for LDAP Plain Text Password Capture]({{ site.url }}{{ site.baseurl }}/assets/images/2015-10-22-openldap-for-ldap-plain-text-password-capture/LDAPworm-passwords.png)

I recently tested an application using LDAP to connect to Active Directory to perform queries. The app had valid AD credentials and I wanted to steal them. I couldn't grab the credentials directly, but I could change some of the app configuration, including the IP address of the LDAP server to connect to. That led to "Let's set up a malicious LDAP server to capture credentials!"

There is no metasploit capture ldap module :-( and I didn't have the time to write one. OpenLDAP does support unencrypted, plaintext authentication, but the instructions for setting that up are non-existent. So I documented as I went to make this post.

All testing was done using Kali Linux, so it's easy to add to a pentest setup.

Usage
-----

In researching this, I found client LDAP devices to be more common than I thought. One example is printers querying user information from Active Directory. Printers aren't very secure, mostly have default creds to get into them, and they might have an AD username and password. LDAP server IP is usually easy to change. And printers are generally stupid enough to do things like plaintext auth. A few minutes of work for a valid login? One that probably has access to a file share with lots of sensitive documents. Score!

Rant about OpenLDAP configuration madness
-----------------------------------------

_(skip if desired)_

I'm sure there's a reason why OpenLDAP changed from a normal readable configuration file to using ldap queries to update a semi-database-like structure. But from a noob perspective, configuration settings make absolutely no sense. The documentation is lacking and there's no examples of common configurations. Instead, you left to wade through pages of Google results, all of which are exactly not what you're trying to do or use the old .conf system.

What I'm trying to do is not in the OpenLDAP administration guide. I finally found the options I needed through forums and digging into the man pages. Authentication options in particular are poorly documented and confusing. I basically had to try all of them (and combinations of them) to get this working. Trying to actually secure the settings will be equally as difficult.

Authentication
--------------

There are three different authentication methods that can be configured.

* Anonymous: no auth needed
* Simple: plaintext username and password
* SASL: a pluggable authentication system supporting many other  
  methods, including a PLAIN method of plaintext username and  
  password.

I have simple auth working here, and pretty sure I have SASL PLAIN  
working. (I can't actually authenticate with SASL PLAIN, but it  
negotiates the method with the client and I can capture the creds). Good  
enough.

Installation
------------

The best guide for basic installation that I've found is [Install and](https://www.lisenet.com/2014/install-and-configure-an-openldap-server-with-ssl-on-debian-wheezy/)  
[Configure an OpenLDAP Server with SSL on Debian Wheezy](https://www.lisenet.com/2014/install-and-configure-an-openldap-server-with-ssl-on-debian-wheezy/). For more configuration than I have here (like SSL/TLS), look at that one. Here's the essentials.

~~~~
apt-get install slapd ldap-utils
dpkg-reconfigure -p low slapd
~~~~

* Omit OpenLDAP server configuration? **No**
* DNS domain name: **{target AD domain name}**
* Organization name: **{target AD domain name}**
* Administrator password: **{password}** _(Doesn't matter, it won't be used)_
* Database backend to use: **HDB**
* Do you want the database to be removed when slapd is purged? **No**
* Move old database? **Yes**
* Allow LDAPv2 protocol? **Yes** _(Support for less secure protocols...oh yeah!)_

If you do the dpkg-reconfigure more than once, you may have to do:

~~~~
rm -rf /var/backups/unknown-2.4.31-2+deb7u1.ldapdb
~~~~

Start the service

~~~~
service slapd start
~~~~

OpenLDAP by default is non-SSL on port 389. Yay, no encryption to worry about.

Testing what authentication methods are allowed
-----------------------------------------------

~~~~
ldapsearch -H ldap:// -x -LLL -s base -b "" supportedSASLMechanisms
~~~~

Example

~~~~
# ldapsearch -H ldap:// -x -LLL -s base -b "" supportedSASLMechanisms
dn:
supportedSASLMechanisms: DIGEST-MD5
supportedSASLMechanisms: CRAM-MD5
supportedSASLMechanisms: NTLM
~~~~

By default, DIGEST-MD5, CRAM-MD5 and NTLM methods are supported. Let's remove those and add in PLAIN.

Reconfiguring using ldapmodify
------------------------------

The "proper" way to configure is to save the changes you want to make into an LDIF-formatted file (whatever that is), and use the ldapmodify command to commit those changes into the actual configuration.

~~~~
# cat >olcSaslSecProps.ldif
dn: cn=config
replace: olcSaslSecProps
olcSaslSecProps: noanonymous,minssf=0,passcred
~~~~

Here is the ldapmodify command. This uses the internal (loopback-like) ldapi:// interface, which can have different authentication (ala no auth) than the external ldap:// interface.

~~~~
ldapmodify -Y EXTERNAL -H ldapi:// -f ./olcSaslSecProps.ldif
~~~~

Example output from same.

~~~~
# ldapmodify -Y EXTERNAL -H ldapi:// -f ./olcSaslSecProps.ldif
SASL/EXTERNAL authentication started
SASL username: gidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=auth
SASL SSF: 0
modifying entry "cn=config"
~~~~

Restart slapd

~~~~
# service slapd restart
[ ok ] Stopping OpenLDAP: slapd.
[ ok ] Starting OpenLDAP: slapd.
~~~~

See what authentication is supported now.

~~~~
# ldapsearch -H ldap:// -x -LLL -s base -b "" supportedSASLMechanisms
dn:
supportedSASLMechanisms: PLAIN
supportedSASLMechanisms: LOGIN
~~~~

Manual configuration
--------------------

The main configuration file is `/etc/ldap/slapd.d/cn=config.ldif`. It says it shouldn't be manually edited. I did and it worked fine.

Testing Simple Authentication
-----------------------------

The ldapsearch command is good for testing authentication. My test domain was evil.ninja (wish I had actually bought that one!). Change it to whatever you configure. And change the host and the password too, unless your password is also "foo".

~~~~
# ldapsearch -h 10.0.2.5 -p 389 -D "cn=admin,dc=evil,dc=ninja" -w foo -b '' -s base -LLL
dn:
objectClass: top
objectClass: OpenLDAProotDSE
~~~~

Testing SASL PLAIN Authentication
---------------------------------

Done from a different system. The auth failed, but the credentials were captured in wireshark.

~~~~
$ ldapsearch -h 10.0.2.5 -p 389 -U "cn=admin,dc=evil,dc=ninja" -I -Y PLAIN -O none -LLL -b '' -s base
SASL/PLAIN authentication started
SASL Interaction
Please enter your authorization name: admin
Default: cn=admin,dc=evil,dc=ninja
Please enter your authentication name: admin
Please enter your password:
ldap_sasl_interactive_bind_s: Invalid credentials (49)
    additional info: SASL(-13): user not found: Password verification failed
~~~~

Capturing plaintext credentials
-------------------------------

At the end of this, my app didn't support plain text authentication (good for them!) But for those that do, capturing is just opening wireshark on 389/tcp. In the wireshark Capture Options, disable promiscuous mode and set a capture filter of `tcp port 389`. (See image below, except actually uncheck promiscuous mode.)

![wireshark capture options]({{ site.url }}{{ site.baseurl }}/assets/images/2015-10-22-openldap-for-ldap-plain-text-password-capture/wireshark-capture-options.png)

wireshark capture options

Once you capture an authentication in wireshark, it looks like this. This is the simple authentication type. The password is "foo".

![auth-simple]({{ site.url }}{{ site.baseurl }}/assets/images/2015-10-22-openldap-for-ldap-plain-text-password-capture/auth-simple.png)

wireshark capturing LDAP auth-simple authentication

Here's the same same user authenticating with SASL-PLAIN auth.

![auth-sasl-plain]({{ site.url }}{{ site.baseurl }}/assets/images/2015-10-22-openldap-for-ldap-plain-text-password-capture/auth-sasl-plain.png)

wireshark capturing LDAP auth-sasl-plain authentication

Capturing DIGEST-MD5 credentials
--------------------------------

If plaintext credentials don't work, DIGEST-MD5 credentials can be tried. It looks like this is a MD5 of the password with a server-side nonce (salt) added and a client-side nonce (salt) added. With a good GPU, stupid or short passwords (ala 8 characters or less) should be crackable. The default configuration supports this method, and it appears to be the first method tried. If needed, do a `dpkg-reconfigure -p low slapd` to get settings back to defaults.

Capturing NTLM credentials
--------------------------

I found no way to configure OpenLDAP to support just NTLM authentication, but I have a dirty workaround that works. I didn't have any way to test this one to see what the wireshark capture looks like.

This uses the same default configuration as DIGEST-MD5, but deletes the libraries for the methods not wanted.

~~~~
mv /usr/lib/x86_64-linux-gnu/sasl2/libcrammd5.so .
mv /usr/lib/x86_64-linux-gnu/sasl2/libdigestmd5.so .
service slapd restart
~~~~

References
----------

* [OpenLDAP Administrator's Guide](https://www.openldap.org/doc/admin24/guide.html)
* [slapd-config(5)](https://linux.die.net/man/5/slapd-config)
* [Install and Configure an OpenLDAP Server with SSL on Debian Wheezy](https://www.lisenet.com/2014/install-and-configure-an-openldap-server-with-ssl-on-debian-wheezy/)
