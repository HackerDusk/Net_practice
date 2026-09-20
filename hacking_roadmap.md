# Roadmap — Cybersécurité / Hacking éthique

Ce fichier est une **carte**, pas un cours : il donne l'ordre, les raisons, et où pratiquer. Le travail se fait derrière chaque lien.

Il a **deux parties** :

- **PARTIE A — Démarrer** : les fondations, dans l'ordre. Suffisant pour les 3-6 premiers mois.
- **PARTIE B — Aller loin** : ce qui fait passer de « j'ai fait des labs » à « je peux être payé pour ça ».

**Ton matériel** : ThinkPad i7-8565U, 8 Go RAM, Windows 11 + WSL + VirtualBox, Wi-Fi 100 Go/mois. Les notes « campus » s'appliquent quand tu utilises les PC du campus (plus de RAM, goinfre).

## Règles à ne jamais casser
- **Labo isolé** : tes VM en réseau interne ou host-only, jamais exposées à Internet ni à un réseau qui n'est pas à toi.
- **Tu n'attaques que** : tes propres VM, des cibles créées pour ça (CTF, TryHackMe, Hack The Box, PortSwigger, OverTheWire), ou une cible où tu as une **autorisation écrite** avec un périmètre défini (bug bounty, contrat).
- **Sortir du périmètre autorisé est illégal**, même avec de bonnes intentions. Informe-toi sur la législation locale sur la cybercriminalité.
- Ce que je t'apporte : expliquer comment les attaques fonctionnent, t'aider à monter ton labo, corriger ta compréhension, te préparer aux plateformes. Ce que je ne fais pas : t'aider à attaquer une cible réelle sans autorisation, ou écrire des malwares.

---
---

# PARTIE A — Démarrer

## A0. Réseau (en cours avec NetPractice)
**Pourquoi en premier** : chaque attaque et chaque outil (Nmap, Wireshark, ARP spoofing) exploite une hypothèse du réseau, une adresse, une route, une confiance mal placée. Sans ça, tout le reste est du copier-coller de commandes.
**Détails** : voir `netpractice_plan.md` (partie A pour le projet, partie B pour la spé).

## A1. Linux : la vraie base, pas le cosmétique
**Pourquoi** : la plupart des outils de sécurité et des serveurs du monde réel tournent sous Linux. Savoir taper une commande ne sert à rien sans comprendre permissions, processus et logs.
**Sujets** : système de fichiers (`/etc`, `/var/log`, `/proc`), permissions (`chmod`, `chown`, propriétaire/groupe/autres), processus (`ps`, `top`, `kill`), redirections et pipes, scripting bash de base, lecture de logs.
**Ressources** : Linux Journey (gratuit, progressif) ; OverTheWire « Bandit » (wargame en ligne de commande, légal, cible prévue pour ça).
**Sur ton PC** : WSL2 pour t'entraîner au quotidien, sans VM à lancer.
**Exercices** : cherche → `Linux Journey command line course free`

## A2. Ton labo VirtualBox
**Pourquoi** : tu dois observer et attaquer des machines qui t'appartiennent, isolées de ton PC et d'Internet.
**Sur ton PC (8 Go)** :
- Réseau **Host-only** ou **Internal Network** dans VirtualBox : tes VM se parlent entre elles, mais ne sortent ni sur Internet ni sur ton Wi-Fi.
- **Une VM à la fois**, ou deux très légères. Debian/Ubuntu Server sans interface graphique (~1 Go) comme cible ; Kali ou Parrot (~2 Go) comme poste d'attaque. Commence par Debian avant Kali : comprends Linux avant de charger 600 outils que tu ne connais pas.
- Cibles volontairement vulnérables : **Metasploitable2** (VM gratuite conçue pour ça), **DVWA** (appli web vulnérable, dans Docker/WSL).
**Sur les PC du campus (goinfre)** : Kali + Metasploitable2 + une VM Windows en même temps. Le goinfre est généralement un stockage temporaire, non sauvegardé, parfois purgé : exporte tes VM importantes et vérifie les règles de ton campus.
**Exercices** : cherche → `Metasploitable2 VirtualBox host-only network setup tutorial`

## A3. Capturer et lire le trafic (Wireshark)
**Pourquoi** : c'est le pont entre « je connais la théorie TCP/IP » et « je vois ce qui se passe ». Ça démystifie tout le reste.
**Sujets** : filtres de base, reconnaître une requête DNS, une poignée de main TCP, une requête HTTP en clair.
**Exercices** : cherche → `Wireshark tutorial capture http dns tcp handshake for beginners`

## A4. Scan et reconnaissance (Nmap)
**Pourquoi** : un attaquant ou un défenseur cartographie d'abord : quelles machines, quels ports ouverts, quels services. Nmap est un outil, pas de la magie : comprends les types de scan plus que les options.
**Sujets** : scan TCP connect vs SYN, découverte d'hôtes, détection de version de service, sortie lisible (ce qu'un port `filtered` signifie).
**Dans ton labo uniquement** (tes VM, Metasploitable).
**Exercices** : cherche → `Nmap beginner tutorial scan types explained lab practice`

## A5. Chiffrement (concepts)
**Pourquoi** : explique pourquoi certaines attaques échouent (HTTPS vs HTTP) et pourquoi d'autres réussissent (mauvaises configs, mots de passe faibles).
**Sujets** : hash vs chiffrement, symétrique vs asymétrique, TLS et certificats à haut niveau.
**Exercices** : cherche → `symmetric vs asymmetric encryption explained simply TLS basics`

## A6. Vulnérabilités web (le plus rentable pour le bug bounty)
**Pourquoi** : la majorité des failles réelles et des primes viennent du web.
**Sujets** : authentification cassée, contrôle d'accès (IDOR), injection SQL, XSS, SSRF.
**Ressource principale** : **PortSwigger Web Security Academy** (gratuit, labs interactifs). Suis l'ordre du site.

## A7. Documentation (à prendre dès maintenant)
**Pourquoi** : sans notes, un CTF résolu il y a 2 mois est un CTF à refaire.
**Outils** : Obsidian (léger sur 8 Go) ou Cherry Tree.
**Habitude** : note l'objectif, ce que tu as essayé, ce qui a marché, **pourquoi**.

## A8. Première plateforme guidée
**TryHackMe** (progressif, guidé, dans le navigateur ou via VPN, adapté aux débutants) pour appliquer A1 à A6 avec un fil conducteur. Un abonnement n'est pas obligatoire pour démarrer ; beaucoup de salles sont gratuites.

## Ordre de la partie A
Réseau → Linux → labo → Wireshark → Nmap → chiffrement (concepts) → PortSwigger → TryHackMe.

---
---

# ═══════════ LIMITE ═══════════
# Partie A : les fondations pour démarrer.
# Partie B : ce qui fait de toi un professionnel.
# ═══════════════════════════════

---
---

# PARTIE B — Aller loin

## B1. Linux avancé et élévation de privilèges (concept)
**Pourquoi** : une fois « dans » une machine, l'enjeu est d'obtenir plus de droits. Ça exploite presque toujours des mauvaises configurations : permissions trop larges, binaires SUID, tâches `cron`, services mal isolés.
**Sujets** : utilisateurs/groupes, `sudo`, SUID/SGID, `cron`, `systemd`, gestion des paquets, journaux (`journalctl`).
**Où pratiquer** : OverTheWire (Bandit → Leviathan → Narnia), salles « Linux PrivEsc » sur TryHackMe, machines Linux faciles sur Hack The Box.
**Exercices** : cherche → `Linux privilege escalation concepts misconfigurations beginner labs`

## B2. Windows et Active Directory
**Pourquoi** : la majorité des réseaux d'entreprise sont en Windows + Active Directory. C'est là que se trouvent beaucoup d'emplois en pentest et en défense.
**Sujets** : domaine, utilisateurs, groupes, GPO, authentification (NTLM, Kerberos à haut niveau), PowerShell, journaux d'événements.
**Où pratiquer** : parcours Active Directory sur TryHackMe et Hack The Box ; ou ton propre AD (Windows Server d'évaluation en VM, **gros ISO à télécharger au campus, ~10 Go de RAM pour un labo AD complet → PC du campus**).
**Exercices** : cherche → `Active Directory basics concepts lab beginners`

## B3. Web avancé
**Pourquoi** : au-delà des bases (partie A6), les primes viennent des logiques métier, des API et de l'authentification.
**Sujets** : OWASP Top 10, sécurité des API, JWT/OAuth, race conditions, upload de fichiers, désérialisation ; **Burp Suite** (proxy d'interception, l'outil du pentester web).
**Où pratiquer** : PortSwigger en entier, OWASP Juice Shop (en local), DVWA.
**Exercices** : cherche → `OWASP Top 10 explained with labs Burp Suite beginner`

## B4. Méthodologie de pentest et rapport
**Pourquoi** : les clients et les programmes de bug bounty paient pour la **rédaction claire** autant que pour la trouvaille. Un bon rapport (impact, étapes de reproduction, correctif) fait la différence.
**Cycle** : reconnaissance → énumération → exploitation → post-exploitation → rapport. Références : PTES, OWASP Testing Guide.
**Exercices** : après chaque salle/machine, écris un mini-rapport de 1 page. Cherche → `penetration test report example structure`

## B5. Reconnaissance passive / OSINT
**Pourquoi** : on apprend beaucoup sans toucher la cible : sous-domaines, technologies, fuites publiques. Légal quand on reste sur des sources publiques et sur un périmètre autorisé.
**Sujets** : DNS (voir `netpractice_plan.md` B10), certificats publics, moteurs de recherche spécialisés, recherche de secrets dans du code public.
**Exercices** : cherche → `OSINT methodology bug bounty recon beginner`

## B6. Frameworks d'exploitation (Metasploit)
**Pourquoi** : comprendre **ce que fait** un module d'exploitation vaut plus que de lancer `run`. C'est un accélérateur, pas un substitut.
**Sujets** : recherche d'un module, choix de la charge, écouteur, session. Dans ton labo, contre Metasploitable.
**Exercices** : cherche → `Metasploit framework beginner lab Metasploitable2 explained step by step`

## B7. Cryptographie et mots de passe
**Pourquoi** : les identifiants faibles et réutilisés restent la première cause de compromission. Comprendre le hachage, le salage et la force brute explique pourquoi les politiques de mots de passe existent.
**Sujets** : hash, sel, PKI/certificats, gestionnaire de mots de passe, MFA. Dans ton labo, teste la robustesse de **tes propres** hash.
**Exercices** : cherche → `password hashing salting cracking concepts lab`

## B8. Sécurité Wi-Fi
**Pourquoi** : WPA2/WPA3, portails captifs, réseaux invités : un classique des audits.
**Sujets** : chiffrement Wi-Fi, authentification, attaques sur le protocole (concepts). Pratique uniquement sur **ton propre point d'accès**, avec un adaptateur USB compatible.
**Exercices** : cherche → `WPA2 WPA3 security concepts home lab`

## B9. Cloud
**Pourquoi** : la majorité des nouvelles infrastructures. Les failles courantes sont des erreurs de configuration (stockage public, droits IAM trop larges).
**Sujets** : IAM, stockage objet, réseaux virtuels, journaux d'audit. Niveaux gratuits d'AWS, Azure ou GCP.
**Exercices** : cherche → `cloud security beginner misconfigurations IAM labs free`

## B10. Défense (blue team)
**Pourquoi** : il y a plus de postes en défense (SOC, réponse à incident) qu'en attaque, et le défenseur voit ce que l'attaquant laisse comme traces. Comprendre les deux camps fait un meilleur pentester.
**Sujets** : journaux et SIEM (Splunk / Elastic), IDS (Snort, Suricata), Zeek, chasse aux menaces, réponse à incident, durcissement.
**Où pratiquer** : salles SOC Level 1 de TryHackMe, Security Onion en VM, *The Practice of Network Security Monitoring* (Bejtlich).
**Exercices** : cherche → `SOC analyst beginner labs free`

## B11. Analyse de malware (défensive)
**Pourquoi** : comprendre comment un programme malveillant **existant** se comporte, pour le détecter et l'expliquer. C'est un métier de défense.
**Sujets** : analyse statique (chaînes, en-têtes), sandbox, comportement réseau, indicateurs de compromission.
**Règle** : **VM isolée sans aucun accès réseau**, instantané avant chaque test, jamais sur ta machine principale ni sur le réseau du campus.
**Exercices** : cherche → `malware analysis for beginners static analysis sandbox lab`

## B12. Reverse engineering et binaires
**Pourquoi** : comprendre assembleur, mémoire et exploitation de binaires. Indispensable pour la recherche de vulnérabilités bas niveau, moins pour démarrer en bug bounty web.
**Prérequis** : C solide (tes projets 42 t'y préparent), notions d'assembleur x86-64.
**Où pratiquer** : **pwn.college** (cursus gratuit), **crackmes.one**, Ghidra (désassembleur gratuit), gdb. *Les résumés de tes vidéos écrivent « cracks.1 » et « pwn.col » : ce sont très probablement ces deux ressources, vérifie.*
**Exercices** : cherche → `beginner reverse engineering crackme Ghidra tutorial`

## B13. Programmation et automatisation
**Pourquoi** : comprendre comment un logiciel casse, et automatiser les tâches répétitives.
**Ordre** : Python (scripts, `scapy`, `requests`) → Bash → JavaScript (comportement des pages web) → C / assembleur (plus tard). Exercice classique : écrire ton propre scanner de ports ou renifleur simple, **dans ton labo**.
**Exercices** : cherche → `Python for security beginners scapy port scanner lab`

## B14. Plateformes de niveau supérieur
- **Hack The Box** : plus libre et plus dur que TryHackMe ; machines actives et retirées.
- **CTF** : CTFtime.org liste les compétitions ; commence en équipe (voir communauté).
- **Bug bounty** : YesWeHack, Intigriti, HackerOne, Bugcrowd. Lis le **scope** de chaque programme avant de toucher quoi que ce soit.

## B15. Certifications (repère, pas obligation)
- Réseau / bases : Network+, Security+
- Pentest pratique d'entrée : eJPT, puis PNPT
- Référence pratique reconnue : OSCP (long et exigeant)
- Défense : Blue Team Level 1, CySA+
Vérifie les prix actuels, souvent élevés par rapport aux revenus locaux. Aucune n'est nécessaire pour apprendre ; un portfolio solide compte autant pour un premier emploi.

---

## Comment gagner de l'argent (version honnête)
| Voie | Ce que ça demande | Réalité |
|---|---|---|
| Bug bounty | web solide, patience, rapports clairs | premiers mois souvent à zéro, doublons fréquents ; revenus irréguliers |
| Emploi junior (SOC, support sécu, pentest junior) | fondations + portfolio + parfois une certification | la voie la plus stable ; souvent possible à distance |
| Audits pour petites structures | contrat écrit, périmètre clair, rapport propre | possible une fois que tu as des références ; jamais sans autorisation écrite |
| Compétitions / CTF | équipe, régularité | prix rares, mais visibilité et réseau |
Ce qui fait gagner de l'argent : fondations + preuves visibles (write-ups, GitHub, profil TryHackMe/HTB) + patience.

## Portfolio et communauté
- **Write-ups** : un billet par salle/machine résolue (blog, GitHub ou Obsidian publié). Ça remplace un CV quand tu n'as pas d'expérience.
- **Pairs** : ton sujet NetPractice le répète, et c'est vrai en sécu : rejoins les élèves de 42 qui font de la sécu, des équipes CTF, des serveurs Discord de TryHackMe / HTB. Expliquer à quelqu'un révèle tes trous.

## Ta data et ta machine
| Ressource | Ordre de grandeur (à vérifier) |
|---|---|
| Vidéo 480p | ~0,5 Go/h |
| Debian netinst | < 1 Go |
| Ubuntu Server | ~2 Go |
| Kali | ~4 Go |
| Metasploitable2 | < 1 Go |
| ISO Windows Server d'évaluation | quelques Go |
| Wireshark, Packet Tracer | quelques centaines de Mo |
Télécharge les gros fichiers **au campus** et transporte-les sur clé USB. Garde tes 100 Go pour les vidéos et TryHackMe / HTB via VPN.

## Ordre récapitulatif
- **Maintenant** : NetPractice → Linux (WSL) → labo → Wireshark → Nmap → PortSwigger.
- **Ensuite** : TryHackMe → Linux avancé + AD → Burp/web avancé → méthodo + rapports.
- **Puis choisis une voie** : bug bounty web, pentest infra/AD, ou défense (SOC). Reverse engineering, malware et cloud quand les fondations sont solides.
