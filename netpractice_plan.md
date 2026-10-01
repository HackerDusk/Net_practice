# Plan d'étude Réseau — NetPractice + spé sécu

Ce fichier a **deux parties** séparées par une limite claire :

- **PARTIE A — Nécessaire pour le projet NetPractice.** Si tu maîtrises tout ça, tu valides les 10 niveaux et l'évaluation. Rien d'autre n'est demandé.
- **PARTIE B — Pour ceux qui foncent vers la spé sécu.** Ce n'est pas dans NetPractice. Tu la commences quand la partie A est solide (ou en parallèle, 1 ou 2 sujets à la fois, pas plus).

Règle de maîtrise pour chaque sujet : tu peux l'expliquer à voix haute, sans notes, avec un dessin et un exemple. Sinon, tu ne l'as pas encore.

---
---

# PARTIE A — Le projet NetPractice (nécessaire)

## vocabulaire et fondamentaux réseau:
### c'est quoi un réseau ?
Un reseau c'est un ensemble d'appareil capable de communiquer entre eux.
### Qu'est-ce qu'une information envoyée ?
Les ordinateurs manipulent des données sous forme numérique, et ces données doivent être transportées d'un appareil à un autre.
### Premier vocabulaire
- `Host`: Un host est simplement un appareil présent sur un réseau et capable de communiquer sur celui-ci.
- `Client`: rôle qui demande/utilise un service
- `Server`: rôle qui fournit un service
- `internet`: ensemble de réseaux interconnectés

### La différence fondamentale entre PAN, LAN, MAN et WAN:
- PAN (Personal Area Network): c'est une connection a courte distance dedier a des peripheriques personnel connecter entre eux (telephone, montre, mes ecouteur bluetooth).
- LAN = réseau local ; Ethernet et WiFi sont les technologies utilisées pour y faire communiquer les appareils.
- MAN (Metropolitan Area Network) : réseau à l'échelle d'une ville/zone métropolitaine.
  Peut interconnecter plusieurs LAN, mais ce n'est pas sa définition — juste un usage fréquent.
- WAN (Wide Area Network) : réseau à grande échelle géographique (région, pays, continent).
  Peut interconnecter des LAN, des MAN, ou d'autres WAN.

### Est-ce qu'Internet est simplement « un WAN » ? Pourquoi ?
- NON, l'internet n'est pas simplement un WAN, d'ailleur c'est surtout une representation parfaite d'un WAN + une inetsection entre pleusieur type de reseau (reseau des reseau).

### Deux ordinateurs dans la même maison : quel type de réseau pourrais-tu avoir ?
LAN (Local Area Network) ou reseau local ou domestique

## règle route:
Ce qui est déjà sur mon réseau direct → pas de route nécessaire, ça marche tout seul (comme A1 ↔ R1 maintenant).
Pour tout le reste, je dois trouver : quel est le prochain appareil directement joignable par moi qui me rapproche de la destination ? (le next-hop, toujours une IP que je peux déjà atteindre directement — sinon la route est inutilisable).
Ensuite, une seule question tranche le format de la règle :
Est-ce que TOUT ce qui n'est pas chez moi part par le même next-hop ? → une seule règle default suffit, pas besoin de lister chaque réseau.
Est-ce que ça dépend de la destination (plusieurs routeurs, plusieurs chemins possibles) ? → là il faut des routes précises, une par destination/next-hop différent, parce qu'un default unique ne pourrait pas distinguer les deux chemins.
Règle à retenir : si plusieurs routes pourraient matcher une même IP, c'est la plus précise (le masque le plus grand) qui gagne — default n'intervient qu'en dernier recours, quand rien de plus précis ne colle.

Format : destination => next-hop.
Premier (gauche) = ce que tu essaies d'atteindre — un réseau précis (réseau/masque) ou default pour "tout le reste".
Deuxième (droite) = le next-hop — l'IP du voisin directement joignable à qui tu confies le paquet.

Sur les masques par cœur : non, pas besoin de mémoriser une table à part — c'est directement lié à ce que tu maîtrises déjà (bloc = 256 − octet). Le lien : le nombre de bits de masque dans l'octet coupé = combien de fois tu divises 256 par 2 pour arriver à ton bloc.

bloc 128 → 1 bit → /25
bloc 64 → 2 bits → /26
bloc 32 → 3 bits → /27
bloc 16 → 4 bits → /28
bloc 8 → 5 bits → /29
bloc 4 → 6 bits → /30

Et le total CIDR = (nombre d'octets à 255 × 8) + ces bits-là. Ex : 255.255.255.128 → trois octets à 255 (24) + bloc 128 (1 bit) = /25. Ça, ça vaut le coup de le retenir — tu vas t'en servir à chaque niveau.

## A1. Conversion binaire ↔ décimal
[OK]
- **Pourquoi** : tout le reste (masques, sous-réseaux, adresses) repose sur la capacité à lire un octet en binaire instantanément. Sans ça, tu comptes sur tes doigts pendant l'évaluation chronométrée.
- **Exercices** : cherche → `binary to decimal conversion practice exercises subnetting`

## A2. Adresse IPv4 : structure et notation
[OK]
**Pourquoi** : une IP = 32 bits = 4 octets, lue comme « partie réseau + partie hôte ». C'est le socle de tout le projet. Connais aussi les plages privées (`10/8`, `172.16/12`, `192.168/16`) et les adresses spéciales (`127.0.0.0/8` loopback, `169.254.0.0/16` APIPA).
**Exercices** : pas nécessaire si A1 est acquis. C'est de la lecture, pas du calcul.

## A3. Masque de sous-réseau & notation CIDR
[OK]
**Pourquoi** : le masque définit où s'arrête le « réseau » et où commence l'« hôte ». C'est LE concept que NetPractice teste en boucle : chaque champ « Mask » doit être cohérent avec l'IP en face.
**Exercices** : cherche → `CIDR notation subnet mask practice problems with answers`

## A4. Adresse réseau, broadcast, plage utilisable
[OK]
**Pourquoi** : à chaque niveau, tu dois vérifier qu'une IP est dans la plage utilisable de son sous-réseau, et qu'elle n'est ni l'adresse réseau ni le broadcast (pièges fréquents).
**Exercices** : cherche → `subnetting exercises calculate network address broadcast usable range`

## A5. Calcul rapide des puissances de 2 (tailles de bloc)
[OK]
**Pourquoi** : en évaluation, seul `bc` est toléré. Connais par cœur 2^1 à 2^16 pour aller vite.
**Exercices** : cherche → `powers of 2 table subnetting cheat sheet drill`

## A6. VLSM (Variable Length Subnet Masking)
[OK]
**Pourquoi** : plusieurs niveaux imposent des sous-réseaux de tailles différentes. Un lien entre deux routeurs est un sous-réseau à part entière, souvent très petit (par exemple un `/30`). Si tu ne sais pas dimensionner un sous-réseau selon le nombre d'hôtes réellement nécessaires, tu casses le plan d'adressage.
**Exercices** : cherche → `VLSM practice exercises variable length subnet mask examples`

## A7. Rôle du switch vs rôle du routeur
[OK]
**Pourquoi** : le diagramme mélange les deux. Un switch relie des appareils du même réseau (adresses MAC, rien à configurer en IP) ; un routeur relie des réseaux différents et a **une IP par interface**. Les confondre fait échouer un niveau entier sans que tu comprennes pourquoi.
**Exercices** : pas nécessaire. C'est conceptuel : explique-le avec l'analogie rue / carrefour.

## A8. Passerelle par défaut (default gateway)
[OK]
**Pourquoi** : erreur n°1 dans NetPractice. Un hôte ne connaît que son propre réseau ; tout ce qui sort passe par le gateway, qui doit lui-même être **dans le même sous-réseau** que l'hôte.
**Exercices** : refais à voix haute l'exemple « comment réussir la piscine » de tes notes.

## A9. Table de routage & route par défaut (0.0.0.0/0)
[OK]
**Pourquoi** : les routeurs à plusieurs interfaces ont besoin d'une table cohérente. Comprends « destination / next hop », pourquoi `0.0.0.0/0` est le filet de sécurité, et que le routeur choisit la **route la plus spécifique** (préfixe le plus long) quand plusieurs correspondent.
**Exercices** : cherche → `routing table default route longest prefix match practice`

## A10. Lecture des logs de NetPractice (« Forward way »)
[OK]
**Pourquoi** : c'est ton débogueur intégré. Il indique exactement où le paquet meurt (pas d'interface correspondante, pas de route, mauvaise destination). Le lire vite fait gagner un temps énorme en évaluation.
**Exercices** : aucun externe. Casse volontairement une config (change un masque, enlève une route) et observe le message.

## A11. Méthodologie de débogage réseau
[OK]
**Pourquoi** : « IP correcte ? masque cohérent ? gateway dans le même sous-réseau ? route existe ? » est la checklist de tout admin réseau ou pentester. Réutilisable à vie.
**Exercices** : cherche → `network troubleshooting checklist IP addressing common mistakes`

## A12. Modèle OSI (et TCP/IP) — exigé par le README
**Pourquoi** : le sujet impose que la section Resources de ton README mentionne les couches OSI. Au-delà, c'est la carte qui te dit « où vit quoi » quand un truc casse.
**À savoir placer** : couche 1 (câble, Wi-Fi), 2 (Ethernet, MAC, switch), 3 (IP, routeur), 4 (TCP/UDP, ports), 7 (HTTP, DNS, SSH). Les couches 5-6 sont floues en pratique ; connais leur définition, sans y passer des heures. Compare avec le modèle TCP/IP à 4 couches.
**Exercices** : cherche → `OSI model layers real world examples wireshark` puis ouvre une capture Wireshark et pointe chaque en-tête (Ethernet, IP, TCP, HTTP) avec sa couche.

## Avant la soumission
- [ ] 10 niveaux validés, un fichier exporté par niveau (`Get my config`) à la racine du repo
- [ ] Login entré dans l'interface avant chaque export
- [ ] README.md en anglais : 1re ligne en italique avec ton login, Description, Instructions (run.sh, export, 10 fichiers à la racine), Resources (concepts étudiés dont TCP/IP addressing, subnet masks, default gateways, routers and switches, OSI layers + usage de l'IA détaillé)
- [ ] Entraînement en mode « Evaluation » (config aléatoire, chronométré, sans outil externe hors `bc`)

---
---

# ═══════════ LIMITE ═══════════
# Tout ce qui précède suffit pour le projet.
# Tout ce qui suit, c'est pour la spé sécu.
# ═══════════════════════════════

---
---

# PARTIE B — Spé réseau / sécu (au-delà du projet)

Chaque sujet : **Pourquoi** (surtout côté sécu), **Tu maîtrises si**, **Exercices**.

## B1. Encapsulation : comment un message devient une trame
**Pourquoi** : chaque couche ajoute son en-tête (Ethernet → IP → TCP/UDP → données). Comprendre ça, c'est comprendre où un pare-feu, un routeur ou un attaquant regarde, et pourquoi une capture Wireshark se lit de haut en bas.
**Tu maîtrises si** : à partir d'une capture, tu nommes l'en-tête, la couche et les champs clés (MAC src/dst, IP src/dst, TTL, ports).
**Exercices** : cherche → `Wireshark encapsulation headers ethernet ip tcp walkthrough`

## B2. Ethernet, MAC, switching
**Pourquoi** : un switch apprend quelle MAC est sur quel port (table CAM) et diffuse ce qu'il ne connaît pas. Cette mécanique explique le sniffing sur un réseau local, le MAC flooding et la notion de domaine de broadcast.
**Tu maîtrises si** : tu expliques ce que fait un switch quand il reçoit une trame pour une MAC inconnue.
**Exercices** : cherche → `switch MAC address table CAM learning explained packet tracer lab`

## B3. ARP en profondeur
**Pourquoi** : ARP traduit IP → MAC en demandant « qui a cette IP ? » et fait confiance à la réponse, sans authentification. C'est la base de l'ARP spoofing / man-in-the-middle, à étudier **dans ton propre labo**.
**Tu maîtrises si** : tu décris requête, réponse, cache, ARP gratuit, et pourquoi la fausse réponse fonctionne. Défenses à connaître : entrées statiques, Dynamic ARP Inspection sur switches gérés.
**Exercices** : cherche → `ARP request reply wireshark capture explained` puis `ip neigh show` dans ta VM avant et après un ping.

## B4. ICMP, ping, traceroute, TTL
**Pourquoi** : ICMP est l'outil de diagnostic (et de reconnaissance) le plus simple. Le TTL explique comment traceroute cartographie les routeurs traversés.
**Tu maîtrises si** : tu expliques comment `traceroute` fonctionne avec le TTL.
**Exercices** : cherche → `how traceroute works TTL ICMP time exceeded` ; capture un `ping` et un `traceroute` dans Wireshark.

## B5. TCP en profondeur
**Pourquoi** : poignée de main à 3 temps (SYN, SYN-ACK, ACK), numéros de séquence, drapeaux (SYN, ACK, FIN, RST), états (LISTEN, ESTABLISHED, TIME_WAIT). Un scan SYN de Nmap et un SYN flood sont incompréhensibles sans ça.
**Tu maîtrises si** : tu dessines la poignée de main et la fermeture d'une connexion, et tu dis ce qu'un port ouvert / fermé / filtré renvoie.
**Exercices** : cherche → `TCP three way handshake wireshark lab flags sequence numbers` ; `tcp state diagram explained`

## B6. UDP
**Pourquoi** : sans connexion, rapide, sans garantie. DNS, DHCP, NTP, QUIC/HTTP3 en dépendent. L'absence de handshake facilite l'usurpation d'IP source, d'où les attaques par amplification (concept à connaître côté défense).
**Tu maîtrises si** : tu expliques quand on choisit UDP plutôt que TCP, avec 3 protocoles réels.
**Exercices** : cherche → `TCP vs UDP differences examples real protocols`

## B7. Ports, sockets, services
**Pourquoi** : un « port ouvert » est un programme qui écoute. Pour un attaquant comme pour un défenseur, la surface d'attaque = la liste des services qui écoutent.
**Tu maîtrises si** : tu lis la sortie de `ss -tulpn` et tu dis quel processus écoute sur quel port et pour quelle interface (`127.0.0.1` vs `0.0.0.0`).
**Exercices** : lance `python3 -m http.server 8000` (le même serveur que NetPractice), regarde-le apparaître dans `ss -tulpn`, puis connecte-toi avec `curl`.

## B8. Qu'est-ce qu'un serveur ?
**Pourquoi** : un serveur n'est pas une machine spéciale, c'est un **programme qui écoute** sur un port et répond à des clients. Le même PC peut en héberger dix. Comprendre ça démystifie la moitié de la sécu : un serveur web, un serveur SSH, un serveur DNS sont des programmes avec des bugs et des mauvaises configs.
**À connaître** : modèle client/serveur ; démon/service (`systemctl`) ; exemples (nginx/Apache, sshd, DNS, DHCP, base de données, partage de fichiers) ; reverse proxy et load balancer ; différence machine physique / VM / conteneur (Docker) ; bases de durcissement (moindre privilège, mises à jour, désactiver ce qui ne sert pas, lire les logs).
**Tu maîtrises si** : tu déroules « comment réussir la piscine » côté serveur : ce qui écoute, sur quel port, ce qui est loggé.
**Exercices** : installe nginx dans une VM (ou WSL), consulte-le avec `curl`, regarde `/var/log/nginx/access.log` et la capture Wireshark de la même requête. Cherche → `nginx beginner setup logs explained`

## B9. DHCP
**Pourquoi** : la machine qui arrive sur le réseau crie « qui me donne une IP ? » en broadcast (DORA : Discover, Offer, Request, Acknowledge). Un faux serveur DHCP (rogue DHCP) peut rediriger tout le trafic d'un réseau : concept à connaître pour défendre.
**Tu maîtrises si** : tu sais quels champs le DHCP fournit (IP, masque, gateway, DNS, durée de bail) et pourquoi la première requête est un broadcast.
**Exercices** : cherche → `DHCP DORA process wireshark capture` ; installe `dnsmasq` dans une VM sur un réseau interne et regarde un client recevoir un bail.

## B10. DNS
**Pourquoi** : DNS traduit les noms en IP et sert aussi à la reconnaissance (sous-domaines, enregistrements), au phishing (domaines usurpés) et à l'exfiltration. Presque tout trafic commence par une requête DNS.
**À connaître** : hiérarchie racine → TLD → serveur faisant autorité ; résolveur récursif ; cache et TTL ; enregistrements A, AAAA, CNAME, MX, NS, TXT, PTR ; UDP 53 (TCP pour les grosses réponses) ; DoH / DoT.
**Tu maîtrises si** : tu prédis la suite de requêtes pour `www.exemple.mg` avec un cache vide.
**Exercices** : `dig +trace exemple.com`, `dig MX`, `nslookup` ; cherche → `DNS resolution step by step dig trace explained`

## B11. NAT / PAT
**Pourquoi** : plusieurs machines privées partagent une IP publique grâce à une table de traduction (ip:port privé ↔ ip:port public). NAT n'est **pas** un pare-feu : il bloque les connexions entrantes non sollicitées par effet de bord, pas par conception. Le port forwarding (DNAT) est le cas inverse.
**Tu maîtrises si** : tu dessines la table NAT pour deux PC qui visitent le même site en même temps.
**Bonus concret** : compare l'IP WAN de ta box avec ce que dit un site « quelle est mon IP ». Si elles diffèrent, ou si la WAN est dans `100.64.0.0/10`, ton opérateur fait du **CGNAT** (NAT chez lui). Tu ne pourras alors pas recevoir de connexions entrantes depuis Internet, ce qui est aussi une protection.
**Exercices** : cherche → `NAT PAT translation table explained` ; `CGNAT how to detect`

## B12. Pare-feu
**Pourquoi** : c'est la première ligne de défense, et ses règles sont un langage à part. Comprendre ce qu'il voit et ce qu'il ignore t'apprend autant à défendre qu'à contourner (dans ton labo).
**À connaître** : sans état vs avec état ; règles évaluées dans l'ordre, première correspondance ; politique par défaut (tout refuser puis autoriser) ; DMZ ; IDS/IPS (Snort, Suricata) ; pare-feu applicatif (WAF).
**Tu maîtrises si** : tu écris des règles pour « le web est accessible, SSH seulement depuis mon réseau interne » et tu prédis ce que bloque chaque ligne.
**Exercices** : `ufw` puis `nftables` dans une VM ; **pfSense** ou **OPNsense** en VM (gros exercice, idéal sur PC campus). Cherche → `firewall rules beginner lab ufw nftables stateful`

## B13. VLAN et segmentation
**Pourquoi** : découper un réseau physique en réseaux logiques (marketing, serveurs, invités) limite les dégâts si une machine est compromise. Concepts : 802.1Q, ports access / trunk, routage inter-VLAN. Attaques à connaître côté défense : VLAN hopping. Un VLAN seul n'est pas une frontière de sécurité complète.
**Tu maîtrises si** : tu expliques comment deux VLAN se parlent (via un routeur ou un switch L3) et pourquoi c'est un bon point de filtrage.
**Exercices** : **Cisco Packet Tracer** (gratuit avec un compte Cisco Networking Academy). Cherche → `packet tracer VLAN trunk inter-VLAN routing lab`

## B14. Routage avancé
**Pourquoi** : NetPractice n'utilise que des routes statiques. Le vrai Internet utilise des protocoles dynamiques : RIP/OSPF à l'intérieur d'une organisation, **BGP** entre opérateurs. Les détournements BGP montrent que la confiance mal placée existe à toutes les échelles.
**Tu maîtrises si** : tu expliques la différence route statique / dynamique et ce qu'est un système autonome (AS).
**Exercices** : Packet Tracer (routage statique puis OSPF de base). Cherche → `OSPF basic configuration packet tracer lab`

## B15. IPv6
**Pourquoi** : déjà déployé partout, et souvent oublié dans les pare-feu (un réseau « sécurisé » en IPv4 peut rester ouvert en IPv6). NDP remplace ARP. Adresses en 128 bits, `/64` par réseau, link-local `fe80::`, auto-configuration (SLAAC).
**Tu maîtrises si** : tu lis une adresse IPv6 abrégée et tu sais quel protocole remplace ARP.
**Exercices** : `ip -6 a` et `ping -6` dans ta VM ; cherche → `IPv6 addressing basics SLAAC link-local practice`

## B16. Protocoles applicatifs
**Pourquoi** : les attaques ciblent presque toujours l'application. Apprends à reconnaître en clair ce qui circule (HTTP, FTP, Telnet) et ce qui est chiffré (HTTPS, SSH).
**À connaître** : HTTP (méthodes, codes d'état, en-têtes, cookies), TLS à haut niveau, SSH (clés), SMTP/IMAP.
**Tu maîtrises si** : tu lis une requête HTTP brute et une réponse, et tu montres ce qui change avec HTTPS dans Wireshark.
**Exercices** : `curl -v http://...` vs `curl -v https://...` ; cherche → `HTTP request response headers explained curl`

## B17. VPN, proxys, tunnels
**Pourquoi** : encapsuler un trafic dans un autre. Utile à connaître pour comprendre ce que voit ou non un défenseur, et comment on accède à un réseau distant.
**Tu maîtrises si** : tu expliques ce qui change dans la capture avant et après une connexion VPN (WireGuard en labo).
**Exercices** : cherche → `WireGuard VPN lab two VMs`

## B18. Outils du réseau à connaître
`ip`, `ss`, `ping`, `traceroute`, `dig`, `curl`, `tcpdump`, **Wireshark**, `nmap`, `nc` (netcat), Packet Tracer, GNS3 (plus lourd).
Chacun est une fenêtre sur un concept : si tu ne peux pas dire quel concept, tu ne connais pas l'outil.

---

## Projet fil rouge (le meilleur exercice de toute la partie B)
Construis et **documente** ce mini-réseau :
1. Deux sous-réseaux (`192.168.10.0/24` et `192.168.20.0/24`), un **routeur** qui les relie (VM Linux avec `ip_forward` activé, ou Packet Tracer).
2. Un **serveur** dans le 2e réseau : nginx + DNS local (`dnsmasq`).
3. Un client qui reçoit son IP par **DHCP**.
4. Une règle de **pare-feu** sur le routeur : le client atteint le web, pas le SSH.
5. **NAT** sur la sortie vers Internet.
6. Capture Wireshark de chaque étape : DHCP, ARP, DNS, TCP, HTTP.
7. Un schéma + une page de notes : ce qui se passe à chaque étape et pourquoi.

**Ressources machine** : VirtualBox, réseaux « Internal Network » pour les tests (ils n'atteignent ni Internet ni ton Wi-Fi). Ajoute une carte NAT le temps d'installer des paquets, puis retire-la. Sur 8 Go, garde les VM à ~512 Mo–1 Go (Debian sans interface graphique). Le montage complet à trois machines tourne mieux sur un PC du campus.

## Ordre conseillé pour la partie B
B1 → B2 → B3 → B4 → B5 → B6 → B7 → B9 → B10 → B11 → B8 → B12 → B13 → B14 → B15 → B16 → B17.
Fais d'abord B1, B3, B5, B9, B10, B11 : ce sont ceux qui apparaissent dans « comment réussir la piscine », et les plus utiles pour lire une capture Wireshark.

## Ressources
- **Professor Messer** : Network+ (gratuit, vidéos courtes, bon fil directeur), puis Security+.
- **Cisco Networking Academy** : cours gratuits + Packet Tracer.
- **Livres** : *Computer Networking: A Top-Down Approach* (Kurose & Ross) pour la logique de chaque couche ; Tanenbaum *Computer Networks* pour aller plus loin ; Bejtlich *The Practice of Network Security Monitoring* pour l'angle défensif.
- **Beej's Guide to Network Programming** (gratuit, en C) : quand tu voudras écrire toi-même un client/serveur, utile pour les projets 42 qui utilisent des sockets.
- **Julia Evans** (jvns.ca) : explications visuelles des outils et concepts réseau.
- **Certifications à viser plus tard** : Network+ ou CCNA (réseau), Security+ (bases sécu). Vérifie les prix actuels : ils sont élevés par rapport aux revenus locaux, et aucune certification n'est nécessaire pour apprendre.

## Ta data (100 Go/mois)
Ordre de grandeur, à vérifier avant de télécharger : vidéo 480p ≈ 0,5 Go/h ; ISO Debian « netinst » < 1 Go ; Ubuntu Server ≈ 2 Go ; Kali ≈ 4 Go ; Packet Tracer et Wireshark : quelques centaines de Mo. Télécharge les gros ISO **au campus** et rapporte-les sur clé USB ; garde ta data pour les vidéos.
