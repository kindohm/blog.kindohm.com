---
layout: post
title: Wobbly Paraphonic Erebus
---

Two of the coolest features of the <a href="http://www.dreadbox-fx.com/erebus/">Dreadbox Erebus</a> is its paraphonic mode and the semi-modular patching. I used its <a href="https://en.wikipedia.org/wiki/Paraphony">paraphony</a> and LFO rate input to create a patch that allowed for some greasy wobbles between a bass note and a simple melody:

<iframe src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/244085387&amp;color=ff5500&amp;auto_play=false&amp;hide_related=false&amp;show_comments=true&amp;show_user=true&amp;show_reposts=false" width="100%" height="166" frameborder="no" scrolling="no"></iframe>

In the rest of this post I'll show how this was made.

First off, I operate from code. I created a basic pattern using Tidal that simulated playing a single low note along with a melody of higher notes. In this case it's an A3 bass note (MIDI note 45), with random notes selected from an A3 phrygian scale for the "melody":
<pre><code>k7 $ whenmod 16 8 (|+| note "-5") $
stack [
note "45/4" |+| dur "4.5",
(|+| note (choose [0,12,12,24])) $ chooseMidi "45" phryg "0*8?" |+| dur "0.15" ]
|+| modwheel (rand)</code></pre>
You can see the bass and melody parts inside the <code>stack</code>. The <code>whenmod 16 8 (|+| note "-5")</code> part just lowers the entire thing by five half steps every eight bars. The <code>modwheel (rand)</code> applies a random mod wheel value on every note that is played.

OK, then on to the Erebus. Some patching and specific knob settings are required to get the specific sound. Here's a picture of the synth in the state when the recording was made:

<p><img src="/images/2016/erebus01.jpg" /></p>

First, the patching:
<ul>
	<li>Envelope out to VCA in</li>
	<li>LFO out to VCF in</li>
	<li>MOD out to LFO/R in</li>
</ul>
The key to this patch is the MOD out to LFO/R in. This allows the random mod wheel value from code to set the LFO rate on the synth. The LFO on the synth controls the filter cutoff, so that's where the wobbles come from.

The a few other key settings:
<ul>
	<li>LFO Rate at about 10 o'clock</li>
	<li>LFO Depth all the way up</li>
	<li>LFO wave type set to triangle</li>
	<li>Osc1 wave length set to 16</li>
	<li>Osc2 wave length set to 4</li>
	<li>Osc mix at 50%</li>
	<li>Filter cutoff around 50%</li>
	<li>Envelope sustain around 50%</li>
	<li>Set unison to paraphonic</li>
</ul>
That's it!

The two-oscillator paraphony is really fun. I imagine there are a lot of quirks and surprises that can come out of this synth's paraphonic mode when code is used to send MIDI notes in unexpected ways. More experiments for the future!
