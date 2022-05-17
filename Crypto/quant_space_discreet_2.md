# Challenge "Quantization, Space & Discreet (1/3)"

## Description

*Mon petit cousin essaie de compresser son image au format JPEG. En plus de ce qu'il sait déjà faire, il a réussi à ajouter une transformée en cosinus discret ^^. Récupérez l'image !*

## Notre solution


cette fois, les données fournies dans les .npy ne sont plus des matrices 2D, mais des matrices  4D de forme: (50, 88, 8, 8)  ou (25, 44, 8, 8)

```python
import numpy as np

y = np.load("chall2_Y.npy")
cb = np.load("chall2_Cb.npy")
cr = np.load("chall2_Cr.npy")

print(y.shape,cb.shape,cr.shape)
```
output: 
> (50, 88, 8, 8) (25, 44, 8, 8) (25, 44, 8, 8)

Il est temps de nous renseigner sur le fonctionnement de la compression d'images pour le format JPEG, on apprend que parmi les premières étapes:
- l'image est coupée en blocs de 8*8 pixels
- la transformée en cosinus discrète (DCT) en 2d est appliquée sur chaque bloc.

notre matrice 4d est logiquement l'image découpée en blocs, sur lesquelles est appliquée la DCT !
on peut alors reconstituer une image en calculant la DCT inverse en 2D pour chaque bloc avec **scipy**, et en reformant l'image,  comme ceci:
```python
from scipy.fftpack import idct
from matplotlib import pyplot as plt

Ywidth,Yheight = Y.shape[0:2]

final_image = np.zeros((Ywidth*8,Yheight*8))

for i in range(Ywidth):
    for j in range(Yheight):
        x,y = i*8,j*8
        final_image[x:x+8,y:y+8] = idct(idct(Y[i][j],axis=0),axis=1) # 2d idct

plt.imshow(final_image)
plt.show()
```
on retrouve le portrait de Mr oogway, accompagné du flag en question... 
![Alt text](img2.png)
`HACKDAY{AS_DISCREET_AS_NINJAS!!!!!!!!}`
:)

