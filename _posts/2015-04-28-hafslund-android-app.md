---
layout: post
title: Hafslund Android app
author: Haakon Sporsheim
date:  2015-04-28 20:00:00
categories: Apps
tags: android app Hafslund sms
---
Some weeks ago I lost my Android phone into a bucket of paint.
It turned out that the phone didn't quite like that.
I turned it off and gave it a good long shower, - then blow dried it for a 15 minutes.
After some hours I turned it on, which I regret.
I should have waited for a day or two - or even try to extract more of the moisture out of it.
Well, it booted - but I noticed something wasn't quite right.
So after some minutes it locked up.
Trying to boot the phone now doesn't work as the kernel seems to be panicking before complete boot.

Anyway, I can boot into recovery and then adb works.
I obviously tried to salvage what was on the SDcard, so I went through the file system.
It was then I made my discovery.
There was a file named `HafslundLog.txt` on the SDcard.
In it I found all my received text messages (SMS) recorded.
Even messages I had deleted.
So obviously this was logged to the file when the message arrived to my phone.
I quickly checked the permissions requested by the [Hafslund app][no.hafslund.energy].
The current version 1.0.4 did request SMS access. Nooo, Hafslund - you amateurs!

[![hafslund log][screenshot]][screenshot]

So, a bit annoyed, I fired off an email to Hafslund.
This is unacceptable. What kind of stupid java developers do they employ?
Next day I got a reply from their customer support asking me to elaborate on the matter.
I replied by repeating the first email and mentioning posting this on social media.

One week later I got a new email where Hafslund thanked me for bringing this to their attention.
A new version would be ready over the summer.
Yesterday I got a phone call, again - thanking me, but now they were about to push a new version to the play store in the coming days.
And yes, today, - April 28th 2015 they updated the app.
It no longer needs access to SMS. Yay! Way to go Hafslund.

However, I'm still one Android phone short. Bummer.

[no.hafslund.energy]: https://play.google.com/store/apps/details?id=no.hafslund.energy
[screenshot]: {{ "/img/Screenshot-from-2015-04-29-210855.png" | prepend: site.baseurl }}
