# Challenge "Packers :) 1/2"

## Description du challenge

je suis un fichier binaire à plusieurs boucliers !

## Notre solution

Le fichier fournis est un executable ELF qui, une fois executé, nous affiche `i am the flag !! u can not reach me !!`.
Un simple `strings reverse_challenge_v2.elf | grep pack` nous révèle cette ligne : `$Info: This file is packed with the UPX executable packer http://upx.sf.net $`

Il m'as donc juste fallu faire un `upx -d reverse_challenge_v2.elf` pour unpack le fichier exécutable, et via un second passage avec `strings reverse_challenge_v2.elf | grep HACK` nous permet de trouver le flag: `HACKDAY{I_th0ug|-|t_i_would_BE_unreachablE!_:(}`
