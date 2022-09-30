# minitidal

Introducción a TidalCycles de Lina Bautista

Lenguaje para hacer música con live coding escrito por Alex Mclean, gracias él y a su infinita paciencia y también a toda la comunidad de toplap.org, especialmente toplap Barcelona.

En  tidalcycles.org tienes toda la información para instalar tidal, miles de tutoriales e información infinita, 
en club.tidalcycles.org tienes un foro donde buscar mas info y resolver dudas de todo tipo. 

Instalar tidal puede ser un proceso fácil o tardar varios días, por eso utilizaremos una versión mini que qorre en la web, creada en la universidad McMaster en canada: 


https://estuary.mcmaster.ca/

De momento vamos a SOLO MODE, dcimos que utilizaremos MiniTidal 



Ejemplo sencillo para comenzar

s

s "bd"


para evaluar presiona: shift + enter o el triángulo



Todos los samples en un patrón son tocados en un ciclo. Mira cómo se distribuyen:



s "bd sn hh bd"
s "bd sn hh cp arpy drum"
s "bd sn hh cp arpy drum bd arpy bass2 feel future"

Todo lo que está dentro de comillas define un patrón dentro de un ciclo
s "bd sd bd sn"


Estamos creando <<<<<<PATRONES>>>>>>>>> con diferentes SAMPLES
vamos a buscarlos: 

https://github.com/tidalcycles/Dirt-Samples

: 

Cambia al tercer sonido de la carpeta
s "birds:3"

Para silenciar:
silence o -- comentar

~ 
s "~ sn:3"  --la tilde crea un silencio.


[]

-- Patrones mas complejos: varios sonidos dentro de un paso de un ciclo:
s "bd casio chink [can can can]"

--Los paréntesis cuadrados agrupan.
s "[bd bd] bd [sn sn sn] sn sn"

,

--Poliritmia, dos patrones a la vez en el mismo ciclo
s "[can can can, casio casio]"


--Cuantas queramos
s "[hh, sn cp sn, arpy:4 arpy:2, ~ cp, ~ ~ casio]"

--repetición
s "bd*2"
s "[clak chin]*2 bd [circus bd:2]/4"
s "[arpy:0 arpy:1 arpy:2 arpy:3]/2"


<>

-- Un paso por ciclo 
s "bd <arpy:1 arpy:2 arpy:3>"



silence

-- <<<<<<<<<<<<<<<<<<FUNCIONES>>>>>>>>>>>>>>>>

-- https://tidalcycles.org/index.php/Category:Functions

 -- utilizamos $ para poner funciones delante

-- Podemos tocar un patron en reversa con rev

 rev $ s "[[bd sn] cp]"

--Podemos acelerar y desacelerar un patrón así:
 slow 2 $ s "[[bd sn] cp]"

slow 0.5 $ sound "[[bd sn] cp]"

s "alphabet"

-- También podemos usar "fast o density" que es lo contradio de "slow"

fast 2 $ s "[[bd sn] cp]"

-- jux!
jux rev $ fast 2 $ s "[[bd sn] cp]"


silence

-- brak redistribuye los sonidos, un ciclo normal y el siguiente lo reproduce a la mitar del ciclo y lo mueve un cuarto de ciclo...
 brak $ sound "feel feel:3"

cada ciclo hace esto:
s "<[feel feel:3][~ feel feel:3 ~]>"

silence

-- <<<<<<<<<<A Higher-order function>>>>>>>>>

-- is a function that accepts a function among its parameters.
-- https://tidalcycles.org/index.php/Category:Higher-order_functions

--tocar en reversa sólo algunas veces
sometimes (rev) $ s "[[bd sn] cp]"

--lo podemos revertir cada 5 ciclos
every 5 (rev) $ s "[[bd sn] cp]"


-- Combinando velocidades:
 every 4 (slow 0.5) $ every 6 (slow 2) $ s "[[bd sn] cp]"



----------- Probemos algunos samples y hagamos algunos patrones---------

--Mas funciones!

--palíndromos
palindrome $ s "newnotes:2 newnotes:3 newnotes:4"

--Podemos cortar los samples con chop:
chop 8 $ s "newnotes:2 newnotes:3 newnotes:4"



--podemos estriar los samples, es un granulador que divide los samples y mezcla los trozos:
every 4 (chop 16) $ s "numbers:0 alphabet:4"



silence


--------------------------------------------------------------------------------
-- <<<Secuenciando funciones>>>>>
-- podemos secuenciar el comportamiento de las funciones también!
chop "<2 4 6>" $ sound "[jvbass drum:4]"



 every "<3 4 5>" (fast "2 4 3") $ s"newnotes:2 newnotes:3 newnotes:4"


slow 2 $ chop "<3 10 20 4 2>" $ s "newnotes:2 newnotes:3 newnotes:4"


striate "<2 10 2 4>" $ s "newnotes:2" --spread

silence



-------------------------------------------------------------------------------

----EFECTOS!!!
--https://tidalcycles.org/index.php/All_effects_and_synths
---Podemos utilizar diferentes efectos para nuestros samples y synths:

s "tok*3"
    # gain "2" -- volumen
    # cutoff "200" -- eq



    --Podemos panearlos:
s "blip*4"
          # pan "0 1"


    --cutoff es un filtro pasa bajos. Le damos la frecuencia de corte en Hertz.
s"jvbass*4" # cutoff "4000"

    -- podemos secuenciar los parámetros de los efectos también
  s "jvbass*4" # cutoff "<70 100 200 300 500 1000 >"

    --Podemos automatizar cambios en los efectos con funciones contínuas (sine, tri, saw)
s "blip*4" # slow 4 (pan sine)


s "blip*4" # cutoff (range 300 1000 $ slow 4 $ sine) # gain "1.5"


silence

--Tenemos filtros de formantes:
s "moog*5"  # vowel "u a i e o"


--cut
s "moog moog:1" # cut "1"

-----

-- <<<<<<<Performance>>>>>>>>>




-- irand escoge un sonido random de la carpeta, rand: numero random entre 0. y 1.
s "glitch*6 [glitch*3]"  # n (irand 19)
# pan (rand)

-- truco para escoger los sonidos de la carpeta mas rapidamente
 n "0 1 [<3 4 6 7> 1]" # sound "arpy"

-- para que suene en cada ciclo:

--degradeBy
degradeBy 0.5 $ sound "moog"

--whenmod
whenmod 8 4 (const silence) $ sound "jungle*4" # n (irand 12)


silence




--TidalCycles es mantenido y expandido por una comunidad muy activa en internet. No dudeis en contactar a la comunidad en caso de dudas, problemas o sugerencias!
-- https://talk.lurk.org/channel/algorithmic-barcelona
-- https://talk.lurk.org/channel/tidal
--el canal de youtube de tidal cycles tiene excelentes tutoriales
