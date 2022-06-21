# SAE 12
## Guide de dépanage réseau pour une machine Linux et Windows (commandes)

Description: Ce guide vous permettra de dépanner n'importe quelle machine ayant un soucis de connexion réseau qu'elle soit sous Linux ou sous Windows. 

<br/>


###  <span style="color:red">SOMMAIRE</span>

1. Listage des actions nécessaires en interne et externe de la machine
2. Explications des commandes sous Linux et Windows
    1. Linux
    2. Windows
<br/>
<br/>
<br/>


#  <span style="color:red">1. Listage des actions nécessaires en interne et externe de la machine</span>
- Vérifier tous les branchements visuellement ou suite à une commande
- Vérifier toutes les adresses (IP, Pacerelle, Route )
- Si mauvaises adresses : les supprimer puis en attribuer des nouvelles
- Vérifier si le problème est résolu



<br/>


# <span style="color:red">2. Explications des commandes sous Linux et Windows  </span>

##    <span style="color:cyan">1. Vérifier les branchements</span> 
Dans un premier temps avant de faire des manipulations diretement sur votre ordinateur il faut vérifier tous les branchements.
- Vérifier si le câble Ethernet de votre machine et bien brnaché des deux côté (machine et réseau). 
<br/><br/>
- Si vous avez accès aux switchs de votre salle via une baie de brassage, vérifier également les branchements. C'est-à-dire de s'assurer que votre machine est bien brnachée sur le bon port. <br/><br/>
- Si cela ne fonctionne toujours pas, vos câbles pourraient être cassés à l'intérieur ou les fiches elles aussi.<br/><br/>



##    <span style="color:cyan">2. Commandes sous Linux</span> 
Ouvrir un terminal (ctrl+alt+t) et taper les commandes suivantes selon votre problème en étant root pour avoir les permissions.
<br/>
<br/>

- Effectuer la configuration du client DHCP de plusieurs interfaces réseau (si possible avec cette commande le problème sera résolu)
```
>> dhclient
```
<br/>

- Vérifie ou définit l'état de l'unité MII (Media Independent Interface) d'une interface réseau
```
>> mii-tool
````
<br/>

- Connaître son adresse IP sur toutes les interfaces réseau
```
>> ifconfig
```
<br/>

- Attribuer une adresse IPv4 sur une interface réseau
```
>> ip addr add "adresse_ip/masque" dev "interface_réseau"
```
<br/>

- Supprimer une adresse IP sur une interfacé réseau
```
>> ip addr flush "adresse_ip/masque" dev "interface_réseau"
```
<br/>

- Activer une interface réseau
```
>> ip link set "interface_réseau" up
```
<br/>

- Connaitre le parcours pour arriver jusqu’à une machine ou adresse
```
>> traceroute "adresse_ip"
```
<br/>

- Ajouter une passerelle par défaut (gateway)
```
>> ip route add default via "adresse_ip"
``` 
<br/>

- Vérifier si tout fonctionne bien
```
>> ping 8.8.8.8
```
<br/>

<span style="color:red"> Si cela ne fonctionne essayez de recommencer ou de trouver un technitien réseau.</span>
<br/>
<br/>

##    <span style="color:cyan">3. Commandes sous Windows</span> 
Ouvrir l'invite de commande en  recherchant avec la loupe.

<br/>

- Connaitre les propriétés IP des cartes réseaux
```
>> ipconfing /all
````
<br/>

- Libérer la configuration IP actuelle
```
>> ipconfig /release
```
<br/>

- Attribuer une nouvelle adresse IP (serveur DHCP)
```
>> ipconfig /renew
```
<br/>

- Changer l’adresse IPv4 de l’interface réseau (manuellement)
```
>> netsh interface
   ipv4 set address name="interface_réseau"
   static "ip_souhaitée/masque passrelle"
```
<br/>

- Déterminer où un paquet s'est arrêté sur le réseau
```
tracert "adresse_ip"
```
<br/>

- Ajouter une route
```
>> route add -p "adresse_ip_destination" MASK "masque_ip_destination" "ip_gateway_carte_réseau" METRIC 3 IF "numéro_carte_réseau"
```
<br/>

- Valider que la route a bien été prise en compte
```
>> route print
```
<br/>

- Vérifier si tout fonctionne bien
```
>> ping 8.8.8.8
```
<br/>
