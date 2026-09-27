# Réponses au Pack avant les levels — 7 exos

### Exercice 1 — Réseau/broadcast/plage (nouveau préfixe)
`10.4.7.130/27` → réseau, broadcast, plage utilisable ?
Dans ma tête (j'arriverai pas sans écrire alors que à l'évaluation c'est encore chaud):
block size = 2^5 = 32 
27 = 11111111.11111111.11111111.11100000
11100000 = 255.255.255.224
ici 224 c'est l'octet significatif
je peux aussi avoire le block size = 256 - 224 = 32
réseau: `10.4.7.32/27` le multiple du block size plus proche de 130 on a 32 * 4 = 128
-> 10.4.7.128
broadcast: 128 + 32 - 1 = 159
-> 10.4.7.159
plage: 10.4.7.129 - 10.4.7.158
oui je sais , c'est long, et je sais pas comment automatiser tout ca dans la tête pour que ca soit rapide.

### Exercice 2 — Même réseau ? (cas piège : proches en apparence)
`172.20.5.10/28` et `172.20.5.30/28` sont-ils sur le même réseau ?
Dans ma tête, je dois voire les plages(donc je dois calculer la plage de chacun)
Pour `172.20.5.10/28`:
block size: 2^4 = 16 (nombre magique)
puisque 0 est multiple de tout nombre on a comme adresse réseau 172.20.5.0
broadcat = 172.20.5.15
plage: = 172.20.5.1 - 172.20.5.14

Pour `172.20.5.30/28`:
block size: 2^4 = 16
réseau: 172.20.5.16
broadcast: 172.20.5.31
plage: 172.20.5.17-172.20.5.30

-> Non (suffit de regarder les plages) mais c'est vraiment tout ca qui se déroule dans ma tête, la raison pour la quelle je precise c'est que je sais pas si ce qui est dans ma tête est la bonne méthode pour réussir et être plus rapide.

### Exercice 3 — Même réseau ? (cas piège inverse : loin en apparence)
`192.168.9.5/26` et `192.168.9.60/26` sont-ils sur le même réseau ?
Pour `192.168.9.5/26`:
-> Dans ma tête (ça devient peut être rapide):
block size: 2^(32 - 26) = 2^6 = 64
plage: 192.168.9.1-192.168.9.62
plus besoins de calcul la réponse est oui car le 2 ème réseau se trouve dans la plage du premier.

### Exercice 4 — Corriger un masque cassé
`10.0.0.65/27` est correct et fixe. Un deuxième host, sur le même lien, a l'IP fixée à `10.0.0.70` mais son masque affiché est `/24` (donc faux). Quel masque doit-il avoir pour être sur le même réseau que le premier ?

-> /27 aussi ca passe (dans ma tête un petit calcul de la plage ca passe seulement un calcul dans la tête pour la première addresse on a 10.0.0.65-10.0.0.126).

### Exercice 5 — Compléter une IP manquante
`192.168.4.9/29` est fixe. Un deuxième host doit être sur le même réseau, masque `/29` imposé. Donne le réseau concerné et une IP valide possible pour ce deuxième host.

-> on a comme plage (juste dans la tête pour les calculs) 192.168.4.9-192.168.4.14 donc juste une addresse entre .10 et .14 inclu.

### Exercice 6 — Lien point-à-point (/30)
Un routeur a `192.168.100.9/30`. Quelle est la seule adresse possible pour l'appareil en face sur ce même lien ?
plage (dans la tête) 192.168.100.9-192.168.100.10
réponse 192.168.100.10.

### Exercice 7 — Réseaux différents : qu'est-ce qu'il manque ?
`192.168.1.10/24` veut joindre `192.168.2.10/24`. Même réseau ? Si non, qu'est-ce qu'il faut configurer côté premier host, et quel appareil rend la connexion possible ?
plage du premier 192.168.1.0-192.168.1.254
Non raison c'est le 1 != 2 je crois, bah il nous faut un routeur.
