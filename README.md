# Sonic Kayak Soundscape

Custom soundscape/sonification for the Sonic Kayak project. The development of this sounddesign was commissioned by [Creative Coding Utrecht](www.creativecodingutrecht.nl).

# Usage

Follow all steps for building the Sonic Kayak here https://github.com/fo-am/sonic-kayaks

1. Clone/download this repo and add the folder `/soundscape` to the `stick/sonickayak/pd` folder (on the usb-stick connected to the rPi)
2. Replace the `sonickayak.pd` and `zone-hydrophone.pd` patchers in the `stick/sonickayak/pd` with the patchers from this repo.
	- Or if you want to use your own `sonickayak.pd` patcher, add the following object `[soundscape/_main-soundscape]` and initialize with a `1` on the left inlet.

# Overview of the sounddesign

There are 4 different instruments in the patch that interact differently with the incoming data from the sensors (water temperature, turbidity, air quality) on the Sonic Kayak.

1. Karplusstrong string synthesis
	- Reacts to the Particular Matter (air quality)
	- A higher value (more particles, poor air quality) results in more distortion and lower notes
	- Autonormalizing initialized at `20 - 70`
2. Arpegiating distorted sinewave synth
	- Reacts to the Water Temperature
	- Warmer water results in a higher melody, more notes and more delay
	- Autonormalizing initialized at `10 - 20`
3. Drone synth from 4 detuned sinewaves with LFO amplitude modulation
	- Reacts to the Turbidity
	- A higher value (cleaner water) results in brighter tones and a smoother amplitude modulation.
	- Autonormalizing initialized at `380 - 450`
4. Percussion rhythm
	- Reacts to the Water Temperature (but local differences/range)
	- Temperature rising results in more percussive sounds and vice versa
	- Autonormalizing initialized at `0 - 0`

The `zone-hydrophone.pd` patcher has 4x onepole lowpass filter steps (`lop~`) after the `adc~` to reduce high frequency noise with a steeper slope from the high gain needed to hear the hydrophone sounds. It also has a softclipping (`tanh~`) in the chain to clip loud sounds softly. The cutoff is set at `3500 Hz` (based on experiment).
