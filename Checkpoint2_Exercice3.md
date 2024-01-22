# RESEAUX



## Question 3.1 - Quel est le matériel réseau A ? 
L'appareil est un switch de niveau 2, permettant aux matériels de même réseau et qui y sont reliés de pouvoir communiquer entre eux . 

## Question 3.2 - Quel est le matériel réseau B ? Quel est son rôle pour le réseau 10.10.0.0/16 ?
L'appareil est un routeur. Pour le réseau 10.10.0.0/16, il peut attribuer des adresses IP dynamiques aux appareils présent ou encore effectuer un routage NAT en cas de connexion au web par exemple. 

## Qusetion 3.3 - Que signifie f0/0 et g1/0 sur l’élément B ?
Ce sont les interfaces d'un routeur, f faisant référence à fastEthernet soit un débit multiple de 100 Mbit/s, g à GigaEthernet soit un débit multiple de 1000 Mbit/s.  

## Question 3.4 - Pour l'ordinateur PC2, que représente /16 dans son adresse IP ?
Cela représente le nombre de bit attribué au réseau, soit ici les deux premiers octets à savoir 10.11 . Les octets .80.2 renseignent l'ID de la machine sur ce même réseau. 

## Question 3.5 - Pour ce même ordinateur, que représente l'adresse 10.10.255.254 ?
Elle ne représente rien, elle ne fait pas partie de son réseau. 

## Question 3.6 - Plage d'adresses our les ordinateur PC1, PC2, et PC5  :

PC1 10.10.4.1/16
PC2 10.11.80.2/16
PC5 10.10.4.7/15

| PC    | Adresse réseau | Adresse broadcast | Plage début | Plage fin     |
|:------|:---------------|:------------------|:------------|:--------------|
| PC1   | 10.10.0.0/16   | 10.10.255.255     | 10.10.0.1   | 10.10.255.254 |
| PC2   | 10.11.0.0/16   | 10.11.255.255     | 10.11.0.1   | 10.11.255.254 |
| PC5   | 10.10.0.0/15   | 10.11.255.255     | 10.10.0.1   | 10.10.255.254 |

## Question 3.7 - En t'aidant des informations que tu as fourni à la question 3.6, et à l'aide de tes connaissances, indique parmi tous les ordinateurs du schéma, lesquels vont pouvoir communiquer entre eux.
Tous peuvent communiquer entre eux, à l'exception du PC5, dont l'adresse réseau est différente. 

## Question 3.8 - De même, indique ceux qui vont pouvoir atteindre le réseau 172.16.5.0/24.
Les mêmes via la passerelle réseau du routeur ( équpement B ) suivante : 10.10.255.254/16, qui appartient au même réseau.

## Question 3.9 - Quelle incidence y-a-t'il pour les ordinateurs PC2 et PC3 si on intervertit leur ports de connexion sur le matériel A ?
Aucune incidence 

## Question 3.10 - On souhaite mettre la configuration IP des ordinateurs en dynamique. Quelles sont les modifications possible ?
On peut se servir du routeur comme DHCP, et lui demander d'attribuer une adresse dynamique à chaque PC. Pour cela ces derniers doivent être paramétrer en dynamique et non statique, et leur réseau doit être déclarer au routeur. 



# WIRESHARK



## Question 3.11 - Sur le paquet N°5, quelle est l'adresse mac du matériel qui initialise la communication ? Déduis-en le nom du matériel.
L'adresse MAC de l'appareil est la suivante -> 00:50:79:66:68:00. Il s'agit du PC1

## Question 3.12 - Est-ce que la communication enregistrée dans cette capture a réussi ? Si oui, indique entre quels matériel, si non indique pourquoi cela n'a pas fonctionné.
La communication a réussi, elle s'est effectuée entre donc le PC1 et le PC4. 

## Question 3.13 - Dans cette capture, à quel matériel correspond le request et le reply ? Donne le nom, l'adresse IP, et l'adresse mac de chaque materiel.

| Matériel  | Adresse IP     | Adresse MAC       | Statut  |
|:----------|:---------------|:------------------|:--------|
| PC1       | 10.10.4.1/16   | 00:50:79:66:68:00 | Request |
| PC4       | 10.11.4.2/16   | 00:50:79:66:68:03 | Reply   |

## Question 3.14 - Dans le paquet N°2, quel est le protocole encapsulé ? Quel est son rôle ?
C'est le protocole ARP qui est utilisé. Il permet la communication entre appareils d'un même réseau local. Via une requête en broadcast, un appareil demande à communiquer avec une adresse MAC "X". Lorsque l'appareil correspondant répond, les adresses IP respectives sont communiquées. 

## Question 3.15 - Quels ont été les rôles des matériels A et B dans cette communication ?
Le switch permet aux appreils qui sont d'un même réseau, et qui y sont branchés, de pouvoir intéragir entre eux. 
Quant au routeur, il a consitué une table ARP définissant le matériel avec son adresse MAC / IP. Permettant aisni d'adresser la requête au matériel concerné. 




## Question 3.16 - Dans cette trame, qui initialise la communication ? Donne l'adresse IP ainsi que le nom du matériel.
La communication est initialisée par le PC2, dont l'adresse IP est 10.11.80.2/16. 

## Question 3.17 - Quel est le protocole encapsulé ? Quel est son rôle ?
Le protocole ICMP est encapsulé. Il consiste à "ping" un autre équipement réseau pour s'assurer qu'une communication puisse être établie. 

## Question 3.18 - Est-ce que cette communication a réussi ? Si oui, indique entre quels matériel, si non indique pourquoi cela n'a pas fonctionné.
La requête a échouée a de multiples reprises, car le PC2 ne peut bénificier de la passerelle par défaut à savoir 10.10.255.254, qui se trouve hors de son rseau. 

## Question 3.19 - Explique la ligne du paquet N° 2
- 0.005840 -> Temps en ms pour envoyer la requête
- 10.10.80.3 -> Adresse IP du matériel effectuant la requête
- 10.11.80.2 -> Adresse IP du matériel destinataire de la requête
- ICMP -> Protocole utilisé dans la requête, ici un ping. 
- 70 -> Longueur en byte / octet de la requête 
- Destination unreachable -> Information mentionnant que la requête n'a pas pu aboutir, le destinataire étant injoignable

## Question 3.20 - Quels ont été les rôles des matériels A et B ?
Le switch est chargé de transmettre le ping au routeur, pour que ce dernier renvoie le signal sur le réseau correspondant ( Passerelle manquante ).

## Question 3.21 - Dans cette trame, donne les noms et les adresses IP des matériels sources et destination.
Le matériel source est le PC2 qui a pour adresse IP 10.10.4.2/16.
Le matériel destination se situe sur Internet avec l'IP 172.16.5.253

## Question 3.22 - Quelles sont les adresses mac source et destination ? Qu'en déduis-tu ?
MAC Source: ca:01:da:d2:00:1c 
MAC Destination: ca:03:9e:ef:00:38
Ces adresses font référence chacune à une interface des deux routeurs. Peut-être la mise en place d'un routage NAT.

## Question 3.23 - A quel emplacement du réseau a été enregistré cette communication ?
Cette communication a été enregistrée entre les deux routeurs. 
