# Challenge "Industrial"

## Description du challenge

Un étrange fichier vient de nous parvenir, essayez de savoir ce qu'il contient

## Notre solution

Le fichier fournis n'avait pas d'extensions, notre premier reflexe à donc été de regarder si le fichier était en fait un fichier textuel, et il se trouve que le fichier était bien textuel !

Et on y trouve ce contenu:

```gcode
M140 S50
M105
M190 S50
...
```

Certains d'entre nous possédant une imprimante 3D, nous avons reconnu le format de données, c'est l'ensemble d'instructions envoyés à une imprimante 3D pour faire fonctionner l'ensemble, le format est nommé le `gcode`.
Nous avons donc ajouté l'extension `.gcode` à la fin du fichier, et regardé son contenu dans des outils en ligne tel que [ce viewer de gcode](https://ncviewer.com/), le flag était donc tous simplement imprimé en 3D.
