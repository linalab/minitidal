# minitidal

Introducción a TidalCycles de Lina Bautista 

[Aquí ](https://www.canva.com/design/DAEB86AOsoo/0P-NQoAKiilMHHv2iFK05Q/view?utm_content=DAEB86AOsoo&utm_campaign=designshare&utm_medium=link&utm_source=publishsharelink "Aquí ")puedes ver la presentación acerca de live coding,

Lenguaje para hacer música con live coding escrito por Alex Mclean, gracias él y a su infinita paciencia y también a toda la comunidad de toplap.org, Alexandra Cárdenas y especialmente a toplap Barcelona.

En  [tidalcycles.org ](http://tidalcycles.org  "tidalcycles.org ")tienes toda la información para instalar tidal, miles de tutoriales e información infinita, 
en club.tidalcycles.org tienes un foro donde buscar mas info y resolver dudas de todo tipo. 

Instalar tidal puede ser un proceso fácil o tardar varios días, por eso utilizaremos una versión mini que qorre en la web, creada en la universidad McMaster en canada: 


[https://estuary.mcmaster.ca/](https://estuary.mcmaster.ca/ "https://estuary.mcmaster.ca/")

De momento vamos a SOLO MODE, decimos que utilizaremos MiniTidal 


# "

Un jemplo sencillo para comenzar:

`s "bd"`

para evaluar presiona: **shift + enter** o el triángulo

Todos los samples en un patrón son tocados en un ciclo. Mira cómo se distribuyen:

`s "bd sn hh bd"`

`s "bd sn hh cp arpy drum"`

`s "bd sn hh cp arpy drum bd arpy bass2 feel future"`

Todo lo que está dentro de comillas define un patrón dentro de un ciclo
s "bd sd bd sn"


Estamos creando patrones con diferentes SAMPLES
vamos a buscarlos: 

https://github.com/tidalcycles/Dirt-Samples

# : 

Cambia al tercer sonido de la carpeta
`s "birds:3"`

# ~
Para silenciar:`silence`
o comentar `--` 

`s "~ sn:3"`  
la tilde `~`  crea un silencio.


# [ ]

-- Patrones mas complejos: varios sonidos dentro de un paso de un ciclo:
`s "bd casio chink [can can can]"`

--Los paréntesis cuadrados agrupan.
`s "[bd bd] bd [sn sn sn] sn sn"`

--Poliritmia, dos patrones a la vez en el mismo ciclo
`s "[can can can, casio casio]"
`
--Cuantas queramos
`s "[hh, sn cp sn, arpy:4 arpy:2, ~ cp, ~ ~ casio]"`

# *
si usamos el mismo sonido podemos abreviar con:
`s "bd*2"`

`s "[clak chin]*2 bd [circus bd:2]/4"`

`s "[arpy:0 arpy:1 arpy:2 arpy:3]/2"`


# <>

Un paso por ciclo 

`s "bd <arpy:1 arpy:2 arpy:3>"`


------------



> Hagamos unas pruebas más antes de continuar...

------------



Ahora incluyamos algunas funciones...


# rev

Podemos tocar un patron en reversa con rev

` rev $ s "[[bd sn] cp]"`

# Slow, fast

Podemos acelerar y desacelerar un patrón así:
` slow 2 $ s "[[bd sn] cp]"`

`slow 0.5 $ sound "[[bd sn] cp]"`



También podemos usar "fast"... lo contradio de "slow"

`fast 2 $ s "[[bd sn] cp]"`

podemos hacer patrones de la velocidad también... ( y de cualquier cosa!)

`fast "2 1 4" $ s "[[bd sn] cp]"`

# jux
Pone el efecto solo en un canal (muy clásico para que todo suene mejor)

`jux rev $ fast 2 $ s "[[bd sn] cp]"`

# brak
brak redistribuye los sonidos, un ciclo normal y el siguiente lo reproduce a la mitar del ciclo y lo mueve un cuarto de ciclo... (otro clásico para instant party combinado con jux...)

` brak $ sound "feel feel:3"`

cada ciclo hace esto:
``s "<[feel feel:3][~ feel feel:3 ~]>"``

------------


> Momento para hacer prueba, ida al baño y/o cigarrito :)

------------

# every, sometimes, ?, degradeBy

Veamos ahora algunas funciones dentro de funciones

tocar en reversa sólo algunas veces
`sometimes (rev) $ s "[[bd sn] cp]"`

lo podemos revertir cada 5 ciclos
`every 5 (rev) $ s "[[bd sn] cp]"`

Combinando velocidades:
` every 4 (slow 0.5) $ every 6 (slow 2) $ s "[[bd sn] cp]"`



Veamos mas funciones útiles...

# chop
Cortar los samples 
`chop 8 $ s "newnotes:2 newnotes:3 newnotes:4"`

podemos estriar los samples,  divide los samples y mezcla los trozos:
`        striate 8 $ s "newnotes:2 newnotes:3 newnotes:4"`



podemos secuenciar el comportamiento de las funciones también!
`chop "<2 4 6>" $ s "[jvbass drum:4]"`

` every "<3 4 5>" (fast "2 4 3") $ s"newnotes:2 newnotes:3 newnotes:4"`

`slow 2 $ chop "<3 10 20 4 2>" $ s "newnotes:2 newnotes:3 newnotes:4"`

`striate "<2 10 2 4>" $ s "newnotes:2" `





-------------------------------------------------------------------------------


# # 

https://tidalcycles.org/docs/reference/audio_effects/
Podemos utilizar diferentes efectos para nuestros samples y synths:

`s "rave*3" # gain "0.7" # cutoff "200"`

Como ves, se pueden sumar diferentes efectos, el volumen con "gain" y el "cutoff" es un filtro pasa bajos, el número cambia la frecuencia.

podemos secuenciar los parámetros de los efectos también

`s "rave*3" # gain "0.7 1 1.5" # cutoff "<200 4000 20000>"`

Podemos panear también, suma esto al patrón anterior:
         `# pan "0.25 0.5 0.75"`

Hay otra manera de automatizar parámetros de los efectos, con funciones contínuas (sine, tri, saw):

`s "rave:1*3" # gain "0.7 1 1.5" # cutoff "<200 4000 20000>" # pan sine`

Sin, tri, saw, rand tienen un rango predefinido de 0 a 1, si quieres cambiarlo hay que defenirlo:

`s "rave:2*3" # gain "0.7 1 1.5" # cutoff (range 50 10000 sine) # pan rand`

Pero veamos algunos efectos más...

Un filtro de formantes, vocal:
`s "moog*5"  # vowel "u a i e o"`



Con cut podemos cortar un sample para que solo dure un ciclo (para que samples mas largos no se superpongan)

`s "moog*5"  # vowel "u a i e o" # cut 1`

`s "rave:1*3" # gain "0.7 1 1.5" # cutoff (range 50 10000 sine) # pan rand # cut 1`


> Quizá antes de seguir es buen momento para salir a ver si está lloviendo, revisar el correo o charlar con otros humanos...

------------

Veamos algunas funciones de probabilidad muy útiles a la hora de tocar: 

# n

n es útil (entre otras cosas) para escoger un sonido de la carpeta rápidamente:

s "alphabet*6" # n "0 3 10 2 7 8"``

podemos combinar n con irand: una funcion que escoge un número rándom entre 0 y el valor que le digamos: 

`jux rev $ s "alphabet*6" # n (irand 20) # cutoff (range 100 5000 sine) `

que tal si ahora incluimos jux rev? y cutoff?

# note

Note cambia el pitch del sample... 
`
jux rev $ s "alphabet*6" # note (irand 20) # cutoff (range 100 5000 sine) `

Quizá esto es mas interesante con algo como: 
`
jux rev $ s "juno*6" # note (irand 20) # cutoff (range 100 5000 sine) `


A proposito, tidal tiene escalas que puedes utilizar: 

# scale


` s "juno*8" # note (scale "major" "0 .. 7") `

Tidal tiene un montón de escalas, y puedes añadir más: 

> minPent majPent ritusen egyptian kumai hirajoshi iwato chinese indian pelog
prometheus scriabin gong shang jiao zhi yu whole wholetone augmented augmented2 hexMajor7 hexDorian hexPhrygian hexSus hexMajor6 hexAeolian major ionian dorian phrygian lydian mixolydian aeolian minor locrian harmonicMinor harmonicMajor melodicMinor melodicMinorDesc melodicMajor bartok hindu todi purvimarva bhairav ahirbhairav superLocrian romanianMinor hungarianMinor neapolitanMinor enigmatic spanish leadingWhole lydianMinor neapolitanMajor locrianMajor diminished octatonic diminished2 octatonic2 messiaen1 messiaen2 messiaen3 messiaen4 messiaen5 messiaen6 messiaen7 chromatic bayati hijaz sikah rast saba iraq

-----


Quizá si ya has llegado a este punto y quieres seguir explorando Tidal, utilizar efectos como delay, reverb, utilizar sintetizadore, midi, etc. es momento de instalar tidal: 

https://tidalcycles.org/







*tidalcycles es mantenido y expandido por una comunidad muy activa en internet. no dudeis en contactar a la comunidad en caso de dudas, problemas o sugerencias, pero también recuerda que hay que investigar antes de lanzarse a preguntar, la respuesta puede estár en algún lugar.... :)*



