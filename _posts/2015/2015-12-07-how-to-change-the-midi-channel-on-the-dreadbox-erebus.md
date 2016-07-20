---
layout: post
title: How to change the MIDI channel on the Dreadbox Erebus
---

I recently picked up a Dreadbox Erebus analog synthesizer. One of the first things I wanted to do was change the MIDI channel that it listens on. According to the owner's manual (as of December 16, 2015), the details about how to do this are on Page 13, but Page 13 does not have these details (doh!). Dreadbox told me they will correct this, but for now I hope this post will shed some light on how to change the MIDI channel.

In short, you need to open the enclosure and locate three DIP switches to change the MIDI channel.

<em>If you go through with this procedure, you do so at your own risk! Please be careful with your beautiful Erebus synth!</em> <em>Disconnect the synth from its power source and any other gear before working on it.</em>

First, you need to remove the bottom cover of the synth's enclosure. There are four screws in the rubber feet; just unscrew them and slide or pull the cover off.

<img src="/images/2015/erebus-channel-01.jpg" />

What you're looking for here is the little red component with three DIP switches:

<img src="/images/2015/erebus-channel-02.jpg" />

By default, these three switches are all OFF, meaning the synth operates in MIDI Omni mode and will listen on all MIDI channels. To get the synth to listen on a specific channel (1-7 only) you will need to turn these switches on in a particular combination.

We're counting in binary here. You can turn the switches on in these combinations to get the proper midi channel:
<pre><code>Switch 1 | Switch 2 | Switch 3 | MIDI Channel
---------------------------------------------
OFF      | OFF      | OFF      | Omni
ON       | OFF      | OFF      | 1
OFF      | ON       | OFF      | 2
ON       | ON       | OFF      | 3
OFF      | OFF      | ON       | 4
ON       | OFF      | ON       | 5
OFF      | ON       | ON       | 6
ON       | ON       | ON       | 7</code></pre>
Here's my synth listening on channel 7:

<img src="/images/2015/erebus-channel-03.jpg" />

After you're done with the switches, just screw the bottom cover back on and you're done!
