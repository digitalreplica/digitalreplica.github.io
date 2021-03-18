---
title:  "AWS Multi-Account SSO Setup Guide"
categories: hacking
excerpt: "You need multiple AWS accounts for hacking. This guide will show you how, using AWS Organizations and SSO."
---
You need multiple AWS accounts for hacking. This guide will show you how, using AWS Organizations and SSO.

# Why?
Hacking requires a lot of tools, and experimentation. Having several AWS accounts lets you keep a "stable" account with working tools, and a playground account that let's you try new things. And let's face it, some of the tools out there aren't quite trustworthy, and keeping those in a separate account reduces your risk. If one account gets compromised, nuke it and spin up a new one.

Larger AWS-based organizations use multiple AWS accounts to separate their envionments, with at least separate development and production accounts. Understanding how they use them will make you a more successful hacker.

# Design
This approach uses Amazon's own management tools for a simple, easy-to use system. The key tools are:

[AWS Organizations](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_introduction.html): Centralized management management and billing for multiple AWS accounts.

[AWS Single Sign-On](https://docs.aws.amazon.com/singlesignon/latest/userguide/what-is.html): Centralized administrator accounts.

Using Organizations, you create a hierarchy of accounts, such as
* Management
  * Tools
  * Playground

# Let's start
The cleanest way to start is with a new AWS account, but this can certainly be used with an existing account as well. You will need two different email addresses:
* Management account root user
* Normal user account

## Management account
The management account controls all the others, and is the first one to set up. This account should only be used for creating other accounts, without any other users, tools, or configuration.

Instructions for setting up a new AWS account are at [New AWS account](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/). The important things to note are:
* Email address: This should be an email that's never been used to sign up for any AWS account, and different than the account you'd like to log in every day with.
* Account name: Name this account something like "management".
* Phone: You'll need a phone number that can receive SMS.

This creates a new account with a special [root user](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html) login. Protect this at all costs, by:
* Setting a long, random password. Save this in your favorite password app
* [Configuring MFA](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html#id_root-user_manage_mfa) for the account.
* And once Single Sign-On is configured, use that for normal login. Save the root user for emergencies only.

### AWS Organizations
Next, turn on AWS Organizations, and set this account as the management account. Use the instructions at [Creating an organization](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_create.html)

Once complete, the AWS Console should show a single account with a star next to it, indicating that this is the management account.

### AWS Single Sign-On
Now, turn on Single Sign-On, using the [Getting started](https://docs.aws.amazon.com/singlesignon/latest/userguide/getting-started.html) guide. The basic steps are:
* Enable AWS SSO
* Use AWS SSO to manage your users

To give yourself access to your accounts, you need to:
* Create an Admins group
* Create a user in the Admins group
* Create a permission set with the AdministratorAccess IAM role
* Assign accounts

**Create Group**
[Add group](https://docs.aws.amazon.com/singlesignon/latest/userguide/addgroups.html)
* Create a group called Administrators

**Create User**
This is the user you'll normally use to log into AWS with.
[Add Users](https://docs.aws.amazon.com/singlesignon/latest/userguide/addusers.html)
* Create a user with your normal email address.
* Add it to the Administrators group

**Create Permission Set**
[create a permission set](https://docs.aws.amazon.com/singlesignon/latest/userguide/howtocreatepermissionset.html).
* Name: AdministratorAccess (or similar)
* Use the "Attach managed policies" button to add the "AdministratorAccess" IAM policy. This gives you full admin access over accounts.

**Assign Users and Permissions**
[Single sign-on access](https://docs.aws.amazon.com/singlesignon/latest/userguide/useraccess.html)
* Select all your AWS accounts and click the "Add Users" button.
* Click the Groups tab and select the Administrators group
* Click the "Permission sets" button and select the AdministratorAccess permission set
* Click Finish

**Find Portal Url**
Single Sign-On creates a portal used to log in and access all your AWS accounts. Be sure to save this url. It will be in the email sent when you created your user, but if you need to find it again.
* Click Dashboard in the menu and look for "User portal URL" at the bottom

## Sign in with normal user account
Log out of the AWS console with your root user. Use the email to log into the user portal with your Single Sign-On user. If everything is successful, you should see an "AWS Account" box, that you can open to access your different accounts.

All of the hard setup stuff is done. Hurray!

# Adding a new AWS account
Now you can use AWS Organizations to create new AWS accounts, then configure Single Sign-On to give yourself access.
* Follow [Creating an AWS account](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_accounts_create.html) to create a new AWS account managed by this account.
* Follow the same steps again in [Single sign-on access](https://docs.aws.amazon.com/singlesignon/latest/userguide/useraccess.html) to select the new account, and add the Administrators group with AdministratorAccess over the new account.
* Refresh your User Portal page. The new account should appear.

Start with a playground or sandbox account. Use this to try different tools and get them working. Once you're happy, create a second account to move stable and tested tools into.

# Finale
Congratulations. You can now take advantage of multiple AWS accounts to hack from. Have fun!
