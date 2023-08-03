# minitidal 

Introduction to TidalCycles by Lina Bautista 


Language to make music with live coding written by Alex Mclean and many more, thanks to him and his infinite patience and also to the entire community of toplap.org, Alexandra Cárdenas and especially to Toplap Barcelona.

In [tidalcycles.org ](http://tidalcycles.org "tidalcycles.org ")you have all the information to install tidal, thousands of tutorials and infinite information, 
In club.tidalcycles.org you have a forum where you can find more info and answer questions of all kinds. 

Installing tidal can be an easy process or take several days, so we will use a mini version that runs on the web, created at McMaster University in Canada: 


[https://estuary.mcmaster.ca/] (https://estuary.mcmaster.ca/ "https://estuary.mcmaster.ca/")

At the moment we are using SOLO MODE, and MiniTidal 


# "

A simple example to get started:

's "BD"'

To evaluate press: **Shift + Enter** or the triangle

All samples in a pattern are played in a cycle. See how they are distributed:

's "BD SN HH BD"'

's "BD SN HH CP Arpy Drum"'

's "BD SN HH CP Arpy Drum BD Arpy Bass2 Feel Future"'

Everything inside quotation marks defines a pattern within a cycle
s "BD SD BD SN"


We are creating patterns with different SAMPLES
Let's look for them: 

https://github.com/tidalcycles/Dirt-Samples

# : 

Switch to the third sound in the folder
's "birds:3"'

# ~
To mute: 'silence'
or comment '--' 

's "~ sn:3"'  
The tilde '~' creates a silence.


# [ ]

-- More complex patterns: several sounds within one step of a cycle:
's "BD Casio Chink [can can can]"'

--Square parentheses group.
's "[BD BD] BD [SN SN SN] SN SN"'

--Polyrhythmia, two patterns at once in the same cycle
's "[can can can, casio casio]"
`
--As many as we want
's "[HH, SN CP SN, ARPY:4 ARPY:2, ~ CP, ~ ~ CASIO]"'

# *
If we use the same sound we can abbreviate with:
's "BD*2"'

's "[clak chin]*2 bd [circus bd:2]/4"'

's "[arpy:0 arpy:1 arpy:2 arpy:3]/2"'


# <>

One step per cycle 

's "BD <ARPY:1 ARPY:2 ARPY:3>"'


------------



> Let's do a few more tests before continuing...

------------

let's include some features...


# rev

We can touch a pattern in reverse with rev

' rev $ s "[[bd sn] cp]"'

# Slow, fast

We can speed up and decelerate such a pattern:
' slow 2 $ s "[[bd sn] cp]"'

'slow 0.5 $ sound "[[bd sn] cp]"'



We can also use "fast"... The opposite of "slow"

'Fast 2 $ s "[[BD SN] CP]"'

We can make speed patterns too... (and anything!)

'fast "2 1 4" $ s "[[bd sn] cp]"'

# jux
Puts the effect only on one channel (very classic to make everything sound better)

'Jux Rev $ fast 2 $ s "[[BD SN] CP]"'

# brak
Brak redistributes sounds, one normal cycle and the next one plays it in the middle of the cycle and moves it a quarter of a cycle... (Another classic for instant party combined with Jux...)

' brak $ sound "feel feel:3"'

Each cycle does this:
''s "<[feel feel:3][~ feel feel:3 ~]>"''


# every, sometimes, ?, degradeBy

Let's now look at some functions within functions

Playing in reverse only sometimes
'sometimes (rev) $ s "[[bd sn] cp]"'

We can reverse it every 5 cycles
'every 5 (rev)$ s "[[bd sn] cp]"'

Combining speeds:
' every 4 (slow 0.5) $ every 6 (slow 2) $ s "[[bd sn] cp]"'



Let's see more useful functions...

# chop
Cut the samples 
'chop 8 $ s "newnotes:2 newnotes:3 newnotes:4"'

We can striate the samples, divide the samples and mix the pieces:
' striate 8 $ s "newnotes:2 newnotes:3 newnotes:4"'



We can sequence the behavior of the functions too!
'chop "<2 4 6>" $ s "[jvbass drum:4]"'

' every "<3 4 5>" (fast "2 4 3") $ s"newnotes:2 newnotes:3 newnotes:4"'

'slow 2 $ chop "<3 10 20 4 2>" $ s "newnotes:2 newnotes:3 newnotes:4"'

'striate' <2 10 2 4>" $ s "newnotes:2" '





-------------------------------------------------------------------------------


# # 

https://tidalcycles.org/docs/reference/audio_effects/
We can use different effects for our samples and synths:

's "rave*3" # gain "0.7" # cutoff "200"'

As you can see, you can add different effects, the volume with "gain" and the "cutoff" is a low pass filter, the number changes the frequency.

We can sequence the parameters of the effects as well

's "rave*3" # gain "0.7 1 1.5" # cutoff "<200 4000 20000>"'

We can also pan, add this to the previous pattern:
         '# bread "0.25 0.5 0.75"'

There is another way to automate effect parameters, with continuous functions (sine, tri, saw):

's "rave:1*3" # gain "0.7 1 1.5" # cutoff "<200 4000 20000>" # pan sine'

Sin, tri, saw, rand have a predefined range from 0 to 1, if you want to change it you have to defend it:

's "rave:2*3" # gain "0.7 1 1.5" # cutoff (range 50 10000 sine) # pan rand'

But let's look at some more effects...

A filter of formants, vowel:
's "moog*5" # vowel "u a i e o"'



With cut we can cut a sample so that it only lasts one cycle (so that longer samples do not overlap)

's "moog*5" # vowel "u a i e o" # cut 1'

's "rave:1*3" # gain "0.7 1 1.5" # cutoff (range 50 10000 sine) # rand bread # cut 1'


------------

Let's look at some very useful probability functions when it comes to playing: 

# n

n is useful (among other things) to choose a sound from the folder quickly:

s "alphabet*6" # n "0 3 10 2 7 8"''

We can combine n with irand: a function that chooses a ranking number between 0 and the value we say: 

'Jux Rev$ S "Alphabet*6" # N (Irand 20) # Cutoff (Range 100 5000 Sine)'

What if we now include Jux Rev? and cutoff?

# note

Note changes the sample pitch... 
`
Jux Rev $ s "Alphabet*6" # Note (Irand 20) # Cutoff (Range 100 5000 Sine) '

Perhaps this is more interesting with something like: 
`
Jux Rev $ s "Juno*6" # Note (Irand 20) # Cutoff (Range 100 5000 Sine) '


By the way, tidal has scales that you can use: 

# scale


' s "juno*8" # note (scale "major" "0 .. 7") '

Tidal has a lot of scales, and you can add more: 

> minPent majPent ritusen egyptian kumai hirajoshi iwato chinese indian pelog
prometheus scriabin gong shang jiao zhi yu whole wholetone augmented augmented2 hexMajor7 hexDorian hexPhrygian hexSus hexMajor6 hexAeolian major ionian dorian phrygian lydian mixolydian aeolian minor locrian harmonicMinor harmonicMajor melodicMinor melodicMinorDesc melodicMajor bartok hindu todi purvimarva bhairav ahirbhairav superLocrian romanianMinor hungarianMinor neapolitanMinor enigmatic spanish leadingWhole lydianMinor neapolitanMajor locrianMajor diminished octatonic diminished2 octatonic2 messiaen1 messiaen2 messiaen3 messiaen4 messiaen5 messiaen6 messiaen7 chromatic bayati hijaz sikah rast saba iraq

-----


Maybe if you have already reached this point and want to continue exploring Tidal, use effects such as delay, reverb, use synthesizer, midi, etc. it is time to install tidal: 

https://tidalcycles.org/







*Tidalcycles is maintained and expanded by a very active community on the Internet. Do not hesitate to contact the community in case of doubts, problems or suggestions, but also remember that you have to investigate before starting to ask, the answer may be somewhere .... :)*



