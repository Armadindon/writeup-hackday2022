# Challenge "QWERTY"

## Description du challenge

Le Flag est tapé des doigts !

## Notre solution

Le fichier fournis est une capture de paquets .pcapng, on y observe un grand nombre de paquets utilisant le protocole "USB".
Sans trop de difficultés (via le titre et la description du challenge), nous avons pu déterminer que ces messages USB étaient des paquets générés lorsque que la personne avait tapé sur son pc.

Grâce à ça, j'ai pu trouvé un lien ayant eu un problème similaire : [Article de Blog](https://blog.stayontarget.org/2019/03/decoding-mixed-case-usb-keystrokes-from.html)

Après avoir récupéré les données des touches pressées (`tshark -r USB.pcap -T fields -e usb.capdata > file.txt`), nous avons donc utilisé le script présent sur l'article et déterminer les touches de claviers utilisées.
Nous avons obtenu : `CapsLockhackdday{u_@CapsLockre-tough!}` que l'on a pu facilement traduire en `HACKDDAY{u_@re-tough!}`
