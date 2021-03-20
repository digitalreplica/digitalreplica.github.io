---
title:  "Can gunshot detection technology contain gun violence?"
categories: seeker
excerpt: "A gunshot detector can be made with 99% accuracy for under $100. Can we use this technology to help contain gun violence?"
---
![Can gunshot detection technology contain gun violence?]({{ site.url }}{{ site.baseurl }}/assets/images/2019-08-10-can-gunshot-detection-technology-contain-gun-violence/microphone.jpg)
*Photo by [Ed Rojas](https://unsplash.com/@ed91?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)*

With more recent mass shootings, we ask once again, "How do we solve gun violence?" Then everyone gets on their soapbox again to blather the same crap about gun control.

What if a better question is "Can we contain gun violence?"

A gunshot detection device can be built **today** for under $100 with 99% accuracy. Reducing police reaction time could potentially save eight lives **on every incident**. Why don't we have them everywhere? Why don't we have our schools bristling with them?

A high school girl can do it
----------------------------
<iframe width="560" height="315" src="https://www.youtube.com/embed/jZMG0VqYnxc" frameborder="0" allow="picture-in-picture" allowfullscreen></iframe>
*A Novel Approach to Gunshot Detection using Internet of Things IoT and Machine Learning*

She built a system using hobby-level electronics that detects gunshots with 99.4% accuracy. It can also determine if the shot came from a handgun or rifle. Read more about her work at [A Novel Approach to Gunshot Detection using Internet of Things (IoT) and Machine Learning - Young Innovators To Watch](https://younginnovatorstowatch.com/entries/a-novel-approach-to-gunshot-detection-using-internet-of-things-iot-and-machine-learning/).

Technology is simply that good now. The sensors, circuits, and computers are absurdly cheap (Arduino and Raspberry Pi). New, readily-available, machine learning algorithms can easily take the data and give probabilities for a handgun fired, a rifle fired, and nothing-happening-here-right-now.

The Dream
---------

Imagine a school. In every classroom and hallway, there's a gunshot detector installed. An incident occurs. Police and school officials know in real-time that a shot has been fired, where it occurred, and what type of weapon. They can track events as they happen: more shots fired, if it moves, if multiple weapons are involved.

Police reaction time is drastically reduced. Evacuation procedures are simplified.

And perhaps this alone would deter someone from going through it.

But it's more complicated than that
-----------------------------------

A group at the Pacific Northwest National Laboratory designed a low-cost [gunshot detection system](https://www.rdmag.com/article/2018/05/sensor-can-instantly-detect-gunshots-id-weapons-during-school-shootings). Their system goes a little further, and can determine the calibre of weapon used. Their estimated cost is less than $100 per device. But they admit that this is just the sensor. There is much more needed to turn this into a viable technology.

### What does it connect to?

If a school installed these, would they connect it to the school alarm system? Would it instantly notify law enforcement? If the goal is to reduce reaction time, then it absolutely has to do both.

It's a bit more complicated than "Call 911". Sending data feeds to law enforcement is a work in progress. We have [Enhanced 911](https://en.wikipedia.org/wiki/Enhanced_9-1-1), but this is a new type of data sent over new channels that would have to be developed and standardized.

### False alarms

They will happen. [Swatting](https://en.wikipedia.org/wiki/Swatting) is a very real problem, where someone prank calls the police to send a SWAT team out to an innocent person's house. Someone will assuredly try to do the same with this. How can we determine when this occurs? What's the penalty if someone does it?

And then there's simply faulty equipment to deal with?

### Certification and maintenance

Can anyone build one of these? Or does it need to go through some sort of certification process?

What does it take to maintain and test these? Is it like a smoke alarm, where someone has to go press a button once a week? There are commercial fire alarm tests that could easily be adapted to cover these types of devices.

None of this is hard. We know how to do this stuff.

Why don't we have these already?
--------------------------------

Good question!

We do. Kinda, maybe, not really.

[ShotSpotter](https://www.shotspotter.com/) is one example of a commercially available system trying to bring gunshot detection to police already. But such systems appear to be **outdoors only**. The accuracy sucks.

From [Gunshot detection system once green-lighted for Richmond isn’t happening](https://www.wric.com/news/taking-action/gunshot-detection-system-once-green-lighted-for-richmond-isnt-happening/):

> An 8News investigation in 2017 did find Shotspotter is not a perfect system. Police using it in other cities were unable to find evidence of gunshots 30% to 70% of the time.

Perhaps the many red light camera and licence plate recognition debacles have made me leery of any company selling technology directly to law enforcement.

Privacy considerations
----------------------

I have serious issues with companies streaming our audio and video out to their systems, where they can use (abuse) it in any way they wish. [Amazon](https://www.cnn.com/2019/04/11/tech/amazon-alexa-listening/index.html), [Google](https://www.inc.com/jason-aten/google-is-absolutely-listening-to-your-conversations-it-just-confirms-why-people-dont-trust-big-tech.html), even [Apple](https://www.theguardian.com/technology/2019/jul/26/apple-contractors-regularly-hear-confidential-details-on-siri-recordings) have plastered the news with their use of your data.

How about a device like this ?

It depends. The first article shows that a [$35 Raspberry Pi](https://www.adafruit.com/product/3775) has enough processing power to perform all analysis on the device itself. No internet connection or streaming of audio needed. It only needs to send an alert when an event happens, with the relevant data.

I'm totally OK with this. Make the data formats open and auditable, respect people's privacy, and no security researcher will have issues with this.

The ability to auto record audio, even video, would be a nice feature to have, **on the device only**. Dashcams are a great example of this. Have an accident and the footage is available to show the police right then and there.

Livestreaming the data out? Well, let's talk.

On my iPhone too?
-----------------

A [Google search](https://www.google.com/search?q=ios+gunshot+detection) finds exactly nothing. Is it possible for Apple to do this? Absolutely!

Apple has extensive experience melding hardware and software to solve similar problems. IOS Photos face detection identifies your friends by [leveraging the power of Apple’s custom-built CPUs and GPUs with deep learning models](https://www.idownloadblog.com/2017/11/16/apple-machine-learning-journal-on-device-facial-recognition/). Saying "Hey Siri" is processed on-device [without sending data to Apple](https://techcrunch.com/2015/09/11/apple-addresses-privacy-questions-about-hey-siri-and-live-photo-features/). All the pieces are already there, and if not, Apple can easily add to next year's model.

Imagine another shooting, this time with dozens of phones detecting and reporting the event. Using location and intensity reading across all of them, the shooter could be pinpointed to within a square foot. Video recording could turn on automatically to gather evidence. The police could see and hear within a second, monitor the situation on-route, and provide real-time instructions to anyone nearby.

Even as a security-nut, I'd probably turn this feature on. If it existed.

### So I asked

I went to Apple's [Product Feedback](https://www.apple.com/feedback/) site to add a feature request to iPhone.

> Please consider adding the ability to iPhones / Siri to detect gunshots, to help protect all Apple users in an active-shooter situation.
>
> As a security-focused consumer, I would like:
>  * all processing on-device
>  * an option to automatically notify law enforcement
>  * an option to automatically turn on video recording
>  * a way to disable it at a gun range
>
>  Thank you,
>
>  Danny

Whether Apple will consider this, who knows. If enough people ask, I think they would.

What can you do?
----------------

Make some noise. Ask for these types of devices.

*   Submit a [Feature Request](https://www.apple.com/feedback/) to Apple iPhone
*   Submit a [Feature Request](https://code.google.com/p/android/issues/entry?template=Feature%20request) for Google Android
*   Submit a [Feature Request](https://forums.developer.amazon.com/topics/feature+request.html) for Amazon Echo
*   Ask schools if they would consider implementing this technology
*   [Contact your elected officials](https://www.usa.gov/elected-officials)
*   Use your own expertise to solve some of the implementation problems
*   Just say that you want it

Conclusion
----------

> If you think technology can solve your security problems, then you don't understand the problems and you don't understand the technology.

**Bruce Schneier** - [Wikiquote](https://en.wikiquote.org/wiki/Bruce_Schneier)

I started with a title using "solve gun violence". This won't.

But can it be used as an effective tool to help contain it? I think it can. Please help.
