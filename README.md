### SC-FreqModulator

Future project: frequency (phase) modulates a signal with its sidechain input

In the analog audio world, frequency modulation with a sine wave is simple enough, and introduces no latency. Surprisingly, more complex waveforms can also be processed in this way, both as the carrier and the modulator. However, in the digital world, complex frequency modulation algorythms are exclusive to expensive VST plugins like Serum or Phase Plant. Even so, these programs use predefined oscillators with clear pitches to define the FM, and it isn't even true FM. (Side note: FM isn't possible in the digital realm, we just recreate it with phase modulation.) This project aims to determine if it even possible to modulate the frequency of one waveform by another, completely unrelated waveform. No more FM'ing saws with sines, we're looking at guitars, voices, and more sounds for more varied sound design purposes. I'm making progress and plan to release this as a VST/AU plugin with the JUCE framework once completed.
-Gage
