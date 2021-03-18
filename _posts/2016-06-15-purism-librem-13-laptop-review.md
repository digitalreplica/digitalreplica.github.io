---
title:  "Purism Librem 13 Laptop Review"
categories: privacy
excerpt: "Review of the Purism Librem 13 laptop for running Qubes OS"
---
![Purism Librem 13 Laptop Review]({{ site.url }}{{ site.baseurl }}/assets/images/2016-06-15-purism-librem-13-laptop-review/l13-v3-turns100.png)

As a security and privacy advocate wanting a new laptop, much time and research was needed to settle on what I wanted. I bought a [Purism Librem 13](https://puri.sm/products/librem-13/) running [Qubes OS](https://www.qubes-os.org/). While this is definitely not the setup for everyone, it is worth considering if you're worried about privacy and have any kind of Linux experience.

So this is a review of the Librem 13 running Qubes with a bundle of setup notes and impressions.

For those not familiar with Qubes, it is the only operating system that is modern, secure and usable. By secure, I mean a machine I trust to log into my financial sites (bank, credit card, etc) and also browse untrusted websites (which given recent website hacks is pretty much everything).

Goals
-----

* Store my files and access my stuff securely.
* Survive untrusted networks.
* Be super portable so I can carry it more places.

Ordering
--------

I ordered at the absolutely worst time, right in the middle of Chinese New Year. I think the lead time was about 2 months. It showed up at random in 4-5 weeks. Not instant gratification, but was happy with the ordering process.

Taking it apart and upgrading things
------------------------------------

The upgrade options while buying the Librem 13 are expensive. Better, cheaper options are available at Newegg or Amazon. I would recommend getting the base model with the hardware kill switches, then upgrading as needed.

Taking it apart
---------------

The bottom is attached with 12 small phillips head screws, arranged in three rows of four. The two center screws are the longest. The lower right corner (assuming the keyboard is closest to you) is slightly longer.

Upgrading
---------

### Ram

Note there is only one RAM slot. I assumed and bought an upgrade that had two memory modules. Oops, had to return and reorder. Past that, is easy to upgrade to 16GB of RAM. I went with a [Crucial 16GB Single DDR3L 1600 Sodimm](https://www.amazon.com/gp/product/B0123BRIDK/).

### Hard Drive

I went with the cheapest hard drive, planning to replace it with an M2 SSD drive. This still turned out cheaper than ordering it with an M2 drive. You can replace the drive with either a 2.5mm SSD or an M2 SSD.

The stock hard drive is a Seagate 500GB Thin drive. This is a 2.5", 7mm drive, so be careful that replacement hard drives are that height. Removing it meant I had to untape and disconnect a small ribbon cable to get to the screws. That was fairly simple, but I was still careful with the cable. Once the hard drive is removed, the bracket can't go back in, so a baggie for storage is needed. Putting the M2 drive was easy, except there's no screw provided. I had to steal one of the hard drive screws.

I later added another 2.5mm SATA SSD to get even more storage. So main OS on the M2 drive and extra storage on the SATA drive. The setup is super quiet, fast and minimal battery drain.

### Power

I already had an Anker 20000mAh battery pack, big enough to power a laptop. All I needed was a cable, so got a [2.5 x 5.5mm Male-to-Male Plug](https://www.amazon.com/gp/product/B00M7OE1VG/) An extra power adapter is also helpful. I ordered the [Toshiba 19V 4.74A 90W Replacement AC Adapter](https://www.amazon.com/gp/product/B005BYUWGC/). Works great.

Qubes on the Librem 13
----------------------

I set up the preloaded Qubes just long enough to test the hardware. My essential tests worked: it connected to the wireless network and sleep worked. Awesome. That's when I replaced the hard drive with the M2 SSD and installed a new Qubes from USB.

Installing Qubes was quick and easy. Everything just worked. I restored VM's from a different machine. I was up and running in 2-3 hours. It would have been faster if I had stayed with the preloaded Qubes.

Observations using it:
----------------------

* All of the special  keys work. This includes brightness, sound, changing monitor configuration, sleep, etc.
* Unplugging and re-plugging external monitors just works. After adjusting the configuration (external monitor only, or both internal/external), the system remembers the settings. Windows resize nicely. The only slightly quirky part is a large windows on an external monitor. When you disconnect, it shrinks to fit the internal display. When reconnecting the external monitor, it's maximized on it (when it wasn't originally). That's mostly not a big deal.
* The HDMI port does support a 4K monitor at full resolution at 30Hz. Nice.
* I have no hard numbers for battery life. With my setup, it seems I can get about 4 hours on battery doing whatever I want with wifi on and screen dimmed a bit.

What I Like
-----------

### Hardware Switches

Love them. I verified that when turning the switch off, the device is removed from the Linux kernel. I mostly keep wireless on and camera off. But it's nice to know that I can switch around as needed.

### Open Hardware

All hardware has support built into the Linux kernel. It just works. Awesome!

### Overall Design

It's small, light. Seems solid and well-made. No issues after throwing it in my bag every day for a while.

What I Dislike
--------------

### Trackpad

The default Qubes driver for it sucks badly. You get the basics like moving, clicking, right-clicking. No other multi-touch gestures work. What's worse is typing. When I'm in a typing groove, some part of my hand hits the trackpad. The cursor jumps all over the place, focus switches to other windows or spaces. It's so bad, I generally use the hotkey to disable the trackpad (yay that you can!) and use a usb mouse. I read that a better driver is in the works. I can't wait.

What I really wish were different
---------------------------------

### Ram

For Qubes, 16GB of ram is the _minimum_ I would consider. I wish the Librem 13 would support 32GB (or more!) I can keep all of my common VMs and some other VM's open. But not everything, so at times I have to close a few to open a few more. It mostly works, but sometimes annoying. PLEASE MORE RAM!

### External Video Connector

The video connector is HDMI. It will drive a 4K monitor at 30Hz. I slightly wish for a DisplayPort, just to get 4K at a full 60Hz.

### Extra Screw for M2 Drive

Please include one extra screw for the M2 slot.

Closing Thoughts
----------------

Would I recommend it? Absolutely. A 32GB version would be pretty close to perfect for a Qubes setup, but this one does very nicely.
