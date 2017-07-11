# Lightpad Block
"Little Foot" programms for the Lightpad Block to use in ROLIs BLOCKS Dashboard Beta 

### a$$_audio_block

I hacked this down in a couple of minutes without checking documentation (mainly because i couldn't find any). It is the same exact 5x5 Melodic Block file, extended by the following features:

#### global
- **Custom Trail Colour**:
You can define a custom Trail colour which will be used regardless of the colour of the pad you hit on (enable "Use custom  trail colour" to take affect).
- **Custom Tonic Colour:** The colour of the tonics can be specified, default is white (enable "Use Custom Tonic Coulour" to take affect)
- **Out of Scale Colour:** Pads which are not in scale are black by default (except for when hide mode is activated). With this option you can define a colour for those notes (a dark gray for example). This way you can see each pad but still know its not on the selected scale (enable "Use custom Out of Scale Colour" to take affect)

#### Scale & key
- **Scale - Custom:** In the scale selector there is a new option called "custom" which lets you select a self defined scale pattern. (Config "Custom Scale")
- **Custom Scale:** Defines the pattern of your custom scale. Because there is no hex input type you will have to enter the integer representation of a three digit hex value.

##### Custom scale

The scale is internally defined as a 3 digit Hex-Value. Or to be more precise a 12 digit bit string. Each of those 12 bits represent a semi tone in the pattern. So 111111111111 (or 0xfff) acivates the pad for each of the twelve semi tones. 

NOTE: It is not possible to define different patterns for the lower/higher octave, the pattern you define repeats for both octaves. (I'm going to look for a workaround on that soon)

The lsb (least significant bit) represents the pad in the lower left corner, going to the right, working its way upwards.
Let's take the (already existing) major pattern as an example.

We want our Lightpad to look like this (0=inactive/1=active):

0 1 0 1 1
0 1 1 0 1
0 1 1 0 1
1 0 1 0 1
1 0 1 0 1

See that the pattern is repeating after the first twelve digits. From bottom left to up right:
101011010101
101011010101
1

Now we just need to inverse the bit string, so that our first pad is the lsb.
=> 101010110101

in hex this comes up to 0xab5

Sadly, the input in ROLI Dashboard only allows for integer inputs, so if you don't want to change this in your .littlefoot file, the "Custom Scale" value must be calculated as an integer. In our case 2741.

It's a bit fiddly, but this makes changing our scale to a self defined pattern possible.


### a$$_mixer_block

Why have a 4 Bar Mixer if you can have one with 5 bars?!
Same exact file as the default Mixer Block Setup for Lightpad, but with a fifth bar and button added to it.

So, instead of four 3px wide bars with a 1px spacing in between, there are five 3px bars without spacing in between. 
It allows for a second slider colour to be selected. This way the sliders have variing colours, making it easier to differentiate.
