# Guide Complet de Documentation Réseau (Débutant)

Ce guide est conçu pour vous expliquer les concepts fondamentaux du réseau comme si vous n'y connaissiez rien. Chaque section inclut des explications simples, des exemples concrets et des liens vers des ressources officielles et académiques pour approfondir.

---

## A6. VLSM (Variable Length Subnet Masking)

### Qu'est-ce que c'est ?
Le **VLSM** (Masquage de sous-réseau de longueur variable) est une technique qui permet de diviser un réseau en morceaux (sous-réseaux) de tailles différentes. 
* **Avant (FLSM)** : Si vous coupiez un gâteau, toutes les parts devaient avoir exactement la même taille, même si un invité avait une toute petite faim et un autre une faim de loup. Cela gaspillait beaucoup d'adresses IP.
* **Avec VLSM** : Vous coupez des parts sur mesure selon le nombre exact de machines (hôtes) dans chaque pièce ou département.

### Exemple concret
Imaginez que vous avez le réseau `192.168.1.0/24` (256 adresses) et trois départements :
1. **Direction** : 50 ordinateurs.
2. **Technique** : 100 ordinateurs.
3. **Secrétariat** : 2 ordinateurs.

Au lieu de faire 3 blocs de 100 (ce qui est impossible avec seulement 256 adresses), le VLSM vous permet de créer :
* Un sous-réseau de 128 adresses pour la Technique (le plus grand d'abord).
* Un sous-réseau de 64 adresses pour la Direction.
* Un tout petit sous-réseau de 4 adresses pour le Secrétariat.

### Ressources pour approfondir
* [Documentation Cisco sur le sous-réseautage et VLSM](https://www.cisco.com/c/fr_ca/support/docs/ip/routing-information-protocol-rip/13788-3.html "Cisco VLSM guide") : Le guide officiel de référence du leader mondial des équipements réseau.
* [Calculateur VLSM en ligne (IPCalculator)](https://www.ipcalculator.net "IP Calculator VLSM tool") : Un outil pratique pour s'exercer à découper vos réseaux automatiquement.

---

## A7. Rôle du Switch vs Rôle du Routeur

Ces deux boîtiers se ressemblent souvent, mais ils ont des rôles totalement différents.

```
[Ordinateur A] ---\                                 /--- [Ordinateur C]
                   >== [ SWITCH A ] === [ ROUTEUR ] === [ SWITCH B ]
[Ordinateur B] ---/                                 \--- [Ordinateur D]
  (Réseau Local 1)                                    (Réseau Local 2)
```

### Le Switch (Le commutateur)
* **Son rôle** : Il crée le réseau local (LAN). Il connecte les appareils entre eux **au sein d'un même bâtiment** ou d'une même pièce.
* **Comment il fonctionne** : Il retient l'adresse physique (appelée **Adresse MAC**) de chaque ordinateur branché sur lui. Quand l'Ordinateur A veut parler à l'Ordinateur B, le switch envoie le message directement sur la bonne prise, sans déranger les autres.
* **Couche OSI** : Il travaille principalement sur la **Couche 2 (Liaison de données)**.

### Le Routeur
* **Son rôle** : Il connecte les réseaux entre eux. C'est la passerelle entre votre réseau local et le reste du monde (Internet).
* **Comment il fonctionne** : Il ne regarde pas les adresses MAC, il regarde les **Adresses IP** (les adresses postales du réseau). Si vous voulez aller sur Google, votre switch local ne sait pas où c'est. Il donne le message au routeur, et le routeur trouve le chemin à travers le monde pour l'envoyer à Google.
* **Couche OSI** : Il travaille sur la **Couche 3 (Réseau)**.

| Fonctionnalité | Switch | Routeur |
| :--- | :--- | :--- |
| **Zone d'action** | Interne (Réseau Local) | Externe (Interconnexion de réseaux) |
| **Identifiant utilisé** | Adresse MAC (Physique) | Adresse IP (Logique) |
| **Composant clé** | Table MAC | Table de routage |

### Ressources pour approfondir
* [Cours OpenClassrooms : Comprendre le rôle du switch et du routeur](https://openclassrooms.com "OpenClassrooms cours reseau") : Une explication pédagogique idéale pour débuter de zéro.

---

## A8. Passerelle par défaut (Default Gateway)

### Qu'est-ce que c'est ?
La **passerelle par défaut** est la porte de sortie de votre réseau local. C'est l'adresse IP de l'interface locale de votre **routeur**.

### Analogie simple
Imaginez que vous êtes dans une pièce (votre réseau local). Vous pouvez parler directement à toutes les personnes dans la pièce. Mais si vous voulez envoyer une lettre à quelqu'un à l'extérieur du bâtiment, vous devez obligatoirement la déposer dans la **boîte aux lettres de la porte de sortie**. Cette porte de sortie, c'est la passerelle.

### Règle d'or absolue
* La passerelle par défaut **doit impérativement être dans le même sous-réseau** que votre ordinateur. 
* Si votre ordinateur a l'IP `192.168.1.5` avec un masque `255.255.255.0`, votre passerelle doit commencer par `192.168.1.X` (souvent `192.168.1.1` ou `192.168.1.254`). Si vous configurez `10.0.0.1` comme passerelle, votre ordinateur sera incapable de la contacter.

### Ressources pour approfondir
* [Support Microsoft : Qu'est-ce qu'une passerelle par défaut ?](https://support.microsoft.com "Microsoft support default gateway") : Définition officielle et explications sur son impact dans Windows.

---

## A9. Table de routage & Route par défaut (0.0.0.0/0)

### La Table de Routage
C'est la carte routière ou le GPS stocké dans la mémoire de votre routeur (ou de votre ordinateur). Chaque fois qu'un paquet de données arrive, le routeur consulte cette table pour savoir où l'envoyer.
Une table de routage contient des règles comme : 
* *"Pour aller vers le réseau des serveurs (10.0.0.0/24), passe par la sortie numéro 2."*

### La Route par Défaut : 0.0.0.0/0
Il est impossible de lister toutes les adresses IP de la Terre entière dans un petit routeur. C'est là qu'intervient la **route par défaut**, écrite `0.0.0.0/0`.

* **Signification** : « Tout ce que je ne connais pas ».
* **Fonctionnement** : Quand le routeur reçoit un paquet pour une destination qui n'est pas écrite explicitement dans sa table (par exemple, le site web d'une université à l'autre bout du monde), il applique la règle `0.0.0.0/0` et envoie le paquet vers son propre fournisseur d'accès à Internet. C'est le choix de secours universel.

### Ressources pour approfondir
* [Documentation d'apprentissage Cloudflare : Qu'est-ce que le routage IP ?](https://www.cloudflare.com/learning/network-layer/what-is-routing/ "Cloudflare learning routing") : Un guide complet et moderne sur le routage et le fonctionnement des tables de routage.

---

## A11. Méthodologie de Débogage Réseau

Quand le réseau "ne marche plus", un bon administrateur ne panique pas et ne cherche pas au hasard. Il suit une checklist logique, du plus proche au plus lointain.

### La Checklist Universelle
1. **IP correcte ?** Mon appareil a-t-il bien reçu une adresse IP ou est-il bloqué sur une adresse d'erreur (ex: `169.254.X.X`) ?
2. **Masque cohérent ?** Le masque correspond-il à celui du réseau pour éviter de s'isoler ?
3. **Gateway dans le même sous-réseau ?** Est-ce que mon IP et l'IP de ma passerelle partagent la même partie réseau ?
4. **La Gateway répond-elle ?** Faire un test de communication (`ping <IP_passerelle>`). Si ça ne répond pas, le problème est local (câble, switch, ou mauvaise IP).
5. **La route existe-t-elle ?** Est-ce que ma table de routage possède bien la route par défaut (`0.0.0.0/0`) pour sortir sur Internet ?
6. **Le DNS fonctionne-t-il ?** Si vous arrivez à faire `ping 1.1.1.1` mais que `ping google.com` échoue, votre connexion fonctionne, c'est juste le traducteur de noms (DNS) qui est en panne.

### Commandes indispensables à tester (Terminal)
* **Windows** : `ipconfig` (voir son IP), `route print` (voir les routes), `ping <cible>`
* **Linux / Mac** : `ip a` ou `ifconfig`, `ip route`, `ping <cible>`

### Ressources pour approfondir
* [Guide de dépannage réseau de la Red Hat Documentation](https://access.redhat.com "Red Hat networking troubleshooting") : Une excellente méthodologie professionnelle pour diagnostiquer les pannes.
* Cherchez sur votre moteur de recherche : `network troubleshooting checklist IP addressing common mistakes` pour trouver des fiches mémos de poche.

---

## A12. Modèle OSI et TCP/IP

Le modèle OSI est un schéma d'organisation en **7 couches** qui explique comment une donnée (comme un clic sur un site web) se transforme en signal électrique ou lumineux pour voyager, puis redevient une donnée sur l'écran d'un autre ordinateur.

### Les Couches Clés à Connaître (Du bas vers le haut)

* **Couche 1 : Physique (Câbles, Wi-Fi, Hubs)**
  * *Rôle* : Transmettre les bits de données purs (0 et 1) sous forme de signaux électriques, lumineux ou radio.
* **Couche 2 : Liaison de données (Ethernet, Adresses MAC, Switch)**
  * *Rôle* : Assurer le transport des données au sein du réseau local d'une machine à une autre via leurs cartes réseau physiques.
* **Couche 3 : Réseau (IP, Routeur, ICMP)**
  * *Rôle* : Gérer l'adressage logique (IP) et trouver le meilleur chemin (routage) pour envoyer les paquets à travers le monde.
* **Couche 4 : Transport (TCP / UDP, Ports)**
  * *Rôle* : S'assurer que les données arrivent en entier et sans erreur (TCP) ou très vite sans contrôle (UDP). Utilise les **numéros de ports** (ex: 80, 443) pour distribuer les données à la bonne application.
* **Couches 5 & 6 : Session & Présentation (Floues en pratique)**
  * *Rôle* : Gèrent la mise en forme (chiffrement, compression) et l'ouverture/fermeture des connexions. En pratique, elles sont souvent fusionnées dans l'application elle-même.
* **Couche 7 : Application (HTTP, DNS, SSH, SMTP)**
  * *Rôle* : C'est l'interface avec laquelle vous interagissez (votre navigateur web utilise le protocole HTTP de cette couche).

### Comparaison avec le modèle TCP/IP (4 couches)
Le modèle théorique OSI est très détaillé, mais le monde réel utilise plutôt le modèle **TCP/IP**, plus compact :
1. **Accès Réseau** (Fusion des couches OSI 1 et 2)
2. **Internet** (Équivalent de la couche OSI 3)
3. **Transport** (Équivalent de la couche OSI 4)
4. **Application** (Fusion des couches OSI 5, 6 et 7)

### Exercice Pratique recommandé
Pour visualiser cela concrètement :
1. Téléchargez le logiciel gratuit [Wireshark](https://www.wireshark.org "Wireshark official site").
2. Lancez une capture de votre réseau et allez sur un site internet non sécurisé ou faites une requête DNS.
3. Cliquez sur une ligne capturée. Vous verrez distinctement l'arborescence des en-têtes qui correspondent pile aux couches : d'abord le bloc Frame (Couche 1/2), puis Ethernet (Couche 2), puis Internet Protocol (Couche 3), puis Transmission Control Protocol (Couche 4), et enfin les données de l'application (Couche 7).

### Ressources pour approfondir
* [Introduction au modèle OSI par Cloudflare](https://www.cloudflare.com/learning/ddos/glossary/open-systems-interconnection-model-osi/ "Cloudflare OSI model guide") : L'explication moderne la plus propre et la plus visuelle disponible sur le web.
