# Challenge "Packers :) 1/2"

## Description du challenge

je suis un fichier binaire à plusieurs boucliers !

## Notre solution

Attention, ce write up est extremement similaire au précédent !

Le fichier fournis est un executable ELF qui, une fois executé, nous affiche `i am the flag !! u can not reach me !!`.
Un simple `strings reverse_challenge_v1.elf | grep pack` nous révèle cette ligne : `$Info: This file is packed with the UPX executable packer http://upx.sf.net $`

Il m'as donc juste fallu faire un `upx -d reverse_challenge_v1.elf` pour unpack le fichier exécutable, et via un second passage avec `strings reverse_challenge_v1.elf | grep =` nous permet de trouver la chaîne `SEFDS0RBWXtVX2cwdF9tRV86KCF9Cg==` qui ressemble à un encodage en base64, avec `echo SEFDS0RBWXtVX2cwdF9tRV86KCF9Cg== | base64 -d` on trouve le flag `HACKDAY{U_g0t_mE_:(!}`
