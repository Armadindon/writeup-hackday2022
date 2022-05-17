# Challenge "Quantization, Space & Discreet (2/3)"

## Description

*"Mon petit cousin essaie de compresser une image au format JPEG, en plus de ce qu'il sait déjà faire, il a réussi à ajouter la quantification à ses coefficients. Récupérez l'image !"*

dans cette 3è partie, on nous donne des fichiers identiques à la seconde partie, plus l'image d'une "matrice 8*8 de quantification" , **Quantization_matrix.png**.

## Notre solution

Maintenant, si l'on lance le script de la partie 2 avec les fichiers fournis dans ce challenge, on obtient un flag trop flou pour être compris.
Après quelques recherches, on comprend que pour réduire la place que prennent les nombres obtenus après dct, l'étape suivante dans la compression jpeg est de diviser chaque coefficient par un nombre et arrondir à l'entier le plus proche


D'après la description du challenge, on déduit que les données fournies sont maintenant les dct après quantification. Si les coeffs des DCTs ont été divisés, on peut retrouver les originales **en multipliant les blocs par la matrice de quantification qui nous est donnée**:

```python
for i in range(Ywidth):
    for j in range(Yheight):
        x,y = i*8,j*8
        final_image[x:x+8,y:y+8] = idct(idct(Y[i][j] * quant_mat ,axis=0),axis=1)

```
Le flag en clair donne `HACKDAY{MASTER_IMG_PREPARATOR¤}`


