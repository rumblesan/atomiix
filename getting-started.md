# Getting Started

This guide is heavily based on the ixi lang help info, with some modifications.

The ixi lang live coding environment is a simple visual system presenting a high entry-level control over synth definitions and samples in SuperCollider. The core idea is to represent events in a spatial layout, thus merging musical code and musical scores, with users assigning scores to named agents to play. The score of an agent is reactive, i.e., if a method is performed upon the score, it changes in real time with those changes reflected in the text file.

Atomiix is a re-implementation of ixi lang, which hopefully manages to make it easier to install and use, without losing too much of its original functionality and charm.

Most of the videos found on www.vimeo.com/ixi should also apply to using Atomiix.

A paper on ixi lang for the 2011 ICMC conference can be found here [www.ixi-audio.net/thor](www.ixi-audio.net/thor).

## Using

Write an agent name, give it a score to play, then evaluate the line by putting the cursor on it and pressing the Ctrl and Enter keys together.


## Scores

There are three different types of scores: melodic mode, rhythmic mode and concrète mode.

### Melodic

```
// square brackets indicate melodic score (synthesis or samples)
agentname  ->   marimba[1    4    3    2    ]
```

Notes are played in a scale from 1 to 9, where 1 is the tonic and spaces represent silence.

### Percussive

```
// vertical lines (pipes) indicate percussive score
agentname  ->   |o   x    o s x   |
```

Samples (or synthdefs) are mapped to keyboard keys with spaces again representing silence.

### Concrete

```
// curly brackets indicate concrète score (samples)
agentname  ->   sndname{0   1   2   8   }
```

Longer samples can be played and their amplitude controlled over the play time. Spaces do not represent silence here.

## Post-score Operators

Scores can be modified by adding operators after the score.

`!` for inserting a silence after the score.
`+` or `-` for transposition in pitch.
`*` or `/` for increasing or decreasing the timing as multiplied or divided by an integer.
`^^` for accents (volume of each note, e.g. `^1418^`).
`()` for note sustain (duration of each note, wholenote = 1, halfnote = 2, quarternote = 4, etc, e.g. `(1)`).
`<>` for panning (1 being the left speaker, 5 middle and 9 the right speaker, e.g, `<15289>`).

All of these will work with melodic and percussive scores, whilst only `!`, `*`, `/` and `<>` will work with concrete scores.

## Commands

### Agent Commands

There are a number of commands that can be used to control and modify the agents and their scores. For all of these, use the name of the command, then the name of the agent, and then further arguments that the command takes, if any.

* doze     Set the agent to sleep.
* wake     Wake the agent, if sleeping.
* nap      Sleep for a N number of seconds. If 2nd argument, then this is repeated N2 times.
           `nap miles 2:4`
* kill     Stop the agent playing and free it.
* shake    Shake the score of an agent, scrambling all items.
* swap     Keep the position of values in the score, but shuffle the values.
* shiftr   Right shift the score by N number of places. Defaults to 1 if no value given.
           `shiftr jimi 6`
* shiftl   Left shift the score by N number of places. Defaults to 1 if no value given.
           `shiftl jimi 2`
* invert   In melodic scores, invert the melody as in twelve-tone technique.
* expand   Expand the score of an agent by N spaces in between notes.
           `expand jimi 2`
* reverse  Reverse the score of an agent.
* up       In percussive scores, this method turns lower case letters to upper case.
* down     In percussive scores, this method turns upper case letters to lower case.
* yoyo     In percussive scores, this method switches the case of all letters.
* order    ?
* replace  ?
* remove   ?
* insert   ?
 
### Global Commands

There are further commands that affect the global state of the environment or editor.

* tonic      Set the tonic of the performance. (as MIDI note value)
* scale      Set the scale of the performance (for all agents evaluated after this event)
* scalepush  Set the scale of the performance (for all agents, including those playing)
* tempo      Set the tempo of performance ( destination tempo: n seconds)
             `tempo 120:2`
* group      Group a number of agents together under one name. This is handy for control.

### Future

The future command allows scheduling events to happen at a specified point in the future. This time can either be a number of seconds, or a number of beats. It's also possible to specify a number of repeats.

This will run the shake command on the jimi agent every two beats, a total of four times.

`future 2b:4 >> shake jimi`

### Editor Commands

* grid   Draw a grid with n spaces which will replace the contents of the line with the command.

## Effects

There are a number of audio effects that can be added to an agent. Currently the parameters on all of them are hard coded but there are plans to change this in future.

* reverb     A decent space reverb 
* reverbS    A small space reverb
* reverbL    A large space reverb
* delay      A decent delay 
* distort    A decent distortion
* cyberpunk  A good healthy effect
* bitcrush   A jolly sounding effect 
* techno     An old trick of sweeping filter
* antique    A lowpass and some vinyl scratches
* lowpass    What it says on the tin 
* tremolo    Amplitude variation
* vibrato    Pitch variation

These can be added to an agent using the `>>` operator and removed using the `<<` operator.

```
jimi  ->   marimba[1    4    3    2    ]

// Add distortion and a reverb effect
jimi >> distort >> reverb

// Remove the distortion
jimi << distort

// add a lowpass filter
jimi >> lowpass

// remove all the effects
jimi <<
```

## Freeing agents

Agents can be freed using the Alt (Command on OSX) and Left keys pressed together. This will stop the agent playing and delete it.


## Structure of a Project

TODO - Add information about projects, keymappings, and custom synthdefs here.

The ixi lang instruments class stores the available instruments. Synthdefs are added when the class is run, but you can use any pattern-ready synth definition you have on your system. Synth Definitions are mapped onto keys on the keyboard, and when the language is run it creates synth definitions with the same names as your samples. This mapping is random unless a special keyMapping.ixi file is present in the sample folder where keys are mapped to the NAME of the sound. Mono and short sounds are ideal.


Use the command "new" go get the GUI where you can create your keymapping file.


If you want to use specific synth definitions for your project and map to the keys, you can create a synthdefs.scd file in your project folder. Make sure you add your synthdefs with the name of the project (e.g., SynthDef(\myDef, {bla bla}).add(\myProject), if you want to be able to map your synthdefs to keys using the keymapping GUI. 


# Example

An example of an Atomiix session with comments .

```
scale minor  // set the scale

// melodic score
jimi     ->       string[1   2    6    2   ]   // here we have an agent called jimi, playing four notes

jimi     ->       string[1   2    6    2   ]+12   // same as above but transposed up an octave (MIDI notes)

jimi     ->       string[1   2    6    2   ]!16   // ! 16 makes silence for 16 notes before playing again

jimi     ->       string[1   2    6    2   ]+12!16(12) // this can be combined - and alternating between whole and half notes

jimi     ->       string[1   2    6    2   ]+12(12~8) //  alternating between whole and half notes but note sustain is multiplied by 8


a -> (135) // a chord can be defined in brackets and assigned to a character (one letter only)

jarret -> piano[1   3   5       a        ] // the chord is then played inside the score

// FIXME what is this!?
a -> $16  // 16 semitones above the fundamental

b -> $24 // two octaves above

c -> (158ab) // a chord with a tonic, a fifth, an octave, a third, and two octave above

bb -> piano[1 2 3 a b c c ]

// or as here below, jack a minor chord into a major scale

scale major

// FIXME
a -> $3

c -> (1a5)

d -> (135)

bb -> piano[1 2 a 3 4 5   c   d   ](1)


// percussive score
ringo    ->             |o   x    o    x   | // here o is mapped to a bass drum and x to a snare drum

ringo2   ->             |      ii   s    n | (1148) // here the notes get durations (two whole notes, a quarter and ab eigth)

ringo3  ->    |c c c c |!2^1219^  // expanded by two and the accents are of amplitude 1 2 1 and 9 (relative to general amp)

ringo4   ->             |       o o d sd   |!12 // ! 12 inserts silence for 12 beats


// concrète score
pierre  ->     water{0        2   8         4    1 0       } // numbers are amplitude

henry  ->     water{0        2   8         }!14 // last amp value is extended by 14 beats

schaeffer ->    water{0        2   8         }*4!14 // duration is multiplied by 4 and same as above


jimi ))   // increase the volume of jimi

jimi >> delay  // add one effect to jimi's output

jimi >> distort >> reverb  // put jimi through distortion and reverb effects

jimi << distort // remove distortion but not the reverb effect

jimi <<  // remove all effects

shake jimi   // scramble jimi's score


future 2:4 >> swap jimi  // in 2 seconds time, swap jimi's score. Do this 4 times

future 2b:4 >> swap jimi  // every 2 bars, swap jimi's score. Do this 4 times

tempo 60  // set the tempo

tempo 120:10 // set the tempo to 120 in 10 seconds


group funnyband -> ringo jimi  // create a new group

doze band  // make the band stop

perk band  // restart the bandmembers

swap jimi   // swap jimi's score


// FIXME doesn't work yet
+ jimi 12  // add 12 as an argument to the score (transposing octave up)

^ jimi 1842  // setting the amplitude arguments of jimi
```
