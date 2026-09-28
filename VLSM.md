exo 1: trouver le bon masque pour un besoin
A:
2^(32 - n) - 2 = 2
2^(32 - n) = 4
2^(32 - n) = 2^2
32 - n = 2
n = 30
nombre d'hotes utlisisables: 2^(32 - 30) - 2 = 2

1 bit = 2^1 possiblilitees car on a soit 0 ou 1
2 bits = 2^2

32 bits = 2^32 et en retir le nombre de bit de reseau qui est n ici
pour le nombre d'hôtes utilisables on retire 2 a cause de l'adresse reseau et broadcast.

B:
2^(32 - n) - 2 = 25
2^(32 - n) = 27
ln(2^(32 - n)) = ln(27)
(32 - n)ln(2) = ln(27)
n = 32 - ln(27)/ln(2)
n = 2
nombre d'hotes utlisisables: 2^(32 - 27) - 2 = 30
bon un peu de gaspiage de 5 reseaux mais c'est pas grave

C:

2^(32 - n) - 2 = 60
2^(32 - n) = 62
n = 32 - (ln(62)/ln(2))
n = 26

nombre d'hotes utilisables: 2^(32 - 26) - 2 = 62
2 addresses gaspillees en plus mais ce n'est pas grave.

D:
2^(32 - n) - 2 = 130
n = 32 - (ln(132)/ln(2))
n = 24
nombre d'hote utilisables: 2^(32 - 24) - 2 = 254

exo 02: retrouver le réseau à partir d'une adresse
A: 192.168.10.77/27

le masque en notation décimale pointée = 255.255.255.224
justification:
echo "ibase=2; 11100000" | bc
224
j'ai calcule l'octet casse
l'adresse réseau = 192.168.10.64
justification:
echo "256-224; 77/32; 77%32" | bc
32
2
13
echo "2*32" | bc
64

alors on a le block size (la taille d'une tranche de reseau) = 32
la tranche ou se trouve le reseau = 2 et reste qui represente la position dans la tranche = 13 en utilisant la methode du nombre magique on peut avoire:
reseau = quotient * bloc (je sais pas mais c'est comme ca qu'on fait)

l'adresse de broadcast = 192.168.10.95
justification:
echo "64+32-1" | bc
95
dans le methode du nombre magique on a
broadcast = addresse reseau + block size - 1

la première et la dernière adresse utilisable:
192.168.10.65-192.168.10.94
car .64 et .95 sont deja prise par reseau et broadcast
le nombre d'hôtes utilisables:
on a 2^(32 - 27) - 2 = 30

B: 10.20.30.200/29

le masque en notation décimale pointée = 255.255.255.248
justification:
echo "ibase=2; 11111000" | bc
248

l'adresse réseau = 10.20.30.200
justification:
echo "256-248; 200/8; 200%8;" | bc
8
25
0
echo "8*25" | bc
200
Oh tient le reseau B est ivalide.il a une addresse reseau.

L'adresse de broadcast = 10.20.30.207
justification:
echo "8*25+8-1" | bc
207

la première et la dernière adresse utilisable:
10.20.30.201-10.20.30.206

le nombre d'hôtes utilisables:
on a 2^(32 - 29) - 2 = 6

C: 172.16.77.9/20

le masque en notation décimale pointée = 255.255.240.0
justification:
echo "ibase=2; 11110000" | bc
240

l'adresse réseau = 172.16.64.0
justification:
 echo "256-240; 77/16; 77%16" | bc
16
4
13
echo "16*4" | bc
64

L'adresse de broadcast = 172.16.79.255
justification:
echo "64+16-1" | bc
79

la première et la dernière adresse utilisable:
172.16.64.1-172.16.79.254

le nombre d'hôtes utilisables:
on a 2^(32 - 20) - 2 = 4094

exo 3: première allocation VLSM complète:
192.168.50.0/24

ordre +  pourquoi:
Wi-Fi, Bureaux,Labo,Serveurs,Lien routeur R2 – R3,Lien routeur R1 – R2
car je pense attaquer les plus grand avant les plus petit.
Pour chacun, donne le préfixe, l'adresse réseau, le broadcast et la plage utilisable.
Wi-Fi:
2^(32 - n) - 2 >= 100
n = 32 - (ln(102)/ln(2)) >= 25
/25 = 255.255.255.128
addresse reseau: 192.168.50.0
addresse broadcast: 192.168.50.127
plage: 192.168.50.1-192.168.50.126

Bureaux:
2^(32 - n) - 2 >= 50
n = 32 - (ln(52)/ln(2)) >= 26
/26 = 255.255.255.192
addresse reseau: 192.168.50.128
addresse broadcast: 192.168.50.191
plage: 192.168.50.129-192.168.50.190

Labo:
2^(32 - n) - 2 = 20
n = 32 - (ln(22)/ln(2)) = 27
/27 = 255.255.255.224
addresse reseau: 192.168.50.192
addresse broadcast: 192.168.50.223
plage: 192.168.50.193-192.168.50.222

Serveurs:
2^(32 - 28) - 2 = 10
n = 32 - (len(12)/ln(2)) = 28
/28 = 255.255.255.240
addresse reseau: 192.168.50.224
addresse broadcast: 192.168.50.239
plage: 192.168.50.225-192.168.50.238

Lien routeur R2 – R3
2^(32-n) - 2 = 2
n = 32 - (ln(4)/ln(2)) = 30
/30 = 255.255.255.252
addresse reseau: 192.168.50.240 
addresse broadcast: 192.168.50.243
plage: 192.168.50.241-192.168.50.242

Lien routeur R1 – R2
2^(32-n) - 2 = 2
n = 32 - (ln(4)/ln(2)) = 30
/30 = 255.255.255.252
addresse reseau: 192.168.50.244 
addresse broadcast: 192.168.50.247
plage: 192.168.50.245-192.168.50.246

Place restant:
block size des 6 sous reseau:
echo "2^(32-25) + 2^(32-26) + 2^(32-27) + 2^(32-28) + 2^(32-30) + 2^(32-30)" | bc
248
ce qui est libre dans le /24:
echo "256-248" | bc
8
cette espace libre commence a .248

exo 4: un bloc plus grand
10.10.0.0/23

Vérification d'abord si tout tient : addition des tailles de blocs avant d'allouer quoi que ce soit.
Campus:
n = 32 - (ln(202)/ln(2)) = 24
bloc = 2^(32 - 24) = 256

Bibliothèque:
n = 32 - (ln(122)/ln(2)) = 25
bloc = 2^(32 - 25) = 128

Administration:
n = 32 - (ln(62)/ln(2)) = 26
bloc = 2^(32 - 26) = 64

Serveurs:
n = 32 - (ln(32)/ln(2)) = 27
bloc = 2^(32 - 27) = 32
3 liens entre routeurs:
*---- * -> 2  
*----- * -> 2
*---- * -> 2
n = 32 - (ln(4)/ln(2)) = 30
bloc = 2^(32 - 30) * 3 = 12

bloc occupe: 492, on est bon

Allocation dans le bon ordre. Pour chaque sous-réseau, donne préfixe, adresse réseau, broadcast et plage utilisable (attention au 3e octet).

Campus:
/24 = 255.255.255.0
adresse réseau = 10.10.0.0
adresse broadcast = 10.10.0.255
plage: 10.10.0.1-10.10.0.254

Bibliothèque:
/25 = 255.255.255.128
adresse réseau = 10.10.1.0
adresse broadcast = 10.10.127.255
plage: 10.10.1.1-10.10.127.254

Administration:
/26 = 255.255.255.192
adresse réseau =
adresse broadcast =
plage:

Serveurs:
/27 = 255.255.255.0
adresse réseau = 10.10.0.0
adresse broadcast = 10.10.0.255
plage: 10.10.0.1-10.10.0.254



Indique ce qu'il reste de libre, et où ça commence.
Fais le schéma.