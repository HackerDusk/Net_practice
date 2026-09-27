# REPRISE_NetPractice_V4.md

## Plan global détaillé

**Phase 0 (maintenant) :** Termine "How networks work" sur networksim (tu es à 18/29, continue jusqu'au bout — ports, protocoles inclus). Ça couvre/renforce directement `netpractice_plan.md` Partie A (A1-A5 déjà acquis, A9-A12 probablement dans ce qui reste du cours) et `hacking_roadmap.md` A0.

**Phase 1 :** Le zip NetPractice (les vrais niveaux) — applique le calcul qu'on a musclé, sur du concret.

**Phase 2 :** Catégorie *"Build and secure a network"* de networksim (VLAN, routage, subnetting pratique/VLSM, DHCP, sécu réseau, capstone "build your first company network"). Ça couvre quasiment toute la Partie B de `netpractice_plan.md` (B1-B13) en un seul endroit cohérent, plutôt que de chercher chaque sujet séparément.

**Phase 3 (en parallèle possible) :** `hacking_roadmap.md` Partie A — Linux (WSL, OverTheWire Bandit), labo VirtualBox, Wireshark, Nmap, PortSwigger, TryHackMe. C'est la pratique manuelle/offensive que networksim ne fait pas (networksim = comprendre, hacking_roadmap = manipuler pour de vrai).

**Phase 4 :** Catégorie *"Security in depth"* de networksim (DPI/IDS, chiffrement en détail, Zero Trust, Wi-Fi sécu) en complément conceptuel de `hacking_roadmap.md` A5, B7, B8.

**Phase 5 :** `hacking_roadmap.md` Partie B (AD, web avancé, méthodo, OSINT, Metasploit, crypto/mdp, cloud, malware, reverse, prog) + catégories *"Operations and incidents"* et *"Specializations"* de networksim (monitoring, incident response, résilience, OSPF, switch/routeur en profondeur, cloud) comme socle théorique pour choisir ta voie (bug bounty / pentest infra / défense SOC).

**Règle unique à garder :** jamais deux fois la même chose en même temps — si networksim couvre déjà un sujet en profondeur, ne va pas chercher un cours vidéo en plus dessus, garde ton temps pour la pratique (labo, TryHackMe, PortSwigger).

## Vérification "vraie vie" — étapes concrètes à faire (annoncées, pas encore exécutées)

1. **Ta propre machine, maintenant.** `ip addr` (Linux) ou `ipconfig` (Windows). Calcule toi-même : bloc, adresse réseau, broadcast, combien de machines maximum sur ce réseau. Recoupe avec le nombre d'appareils connectés affiché par la box.
2. **Ta box internet.** Interface d'admin (souvent `192.168.1.1`), regarde la plage DHCP configurée. Calcule : cohérente avec le masque affiché ? Reste-t-il de la place pour des IP fixes en dehors de cette plage ?
3. **Le vrai test sans filet :** labo VirtualBox (prévu dans `hacking_roadmap.md`) — configurer manuellement l'IP de 2-3 VM (IP statique, masque, passerelle) pour qu'elles se voient sur un réseau interne, sans diagramme, juste `ping` pour vérifier.

Aucun outil supplémentaire à chercher — tu as déjà tout ce qu'il faut (WSL, ta box, VirtualBox prévu). La seule chose qui manque, c'est de le faire une fois par curiosité sur ta propre installation.

## Types d'exercices à connaître et pratiquer

- **A. Vérification express** *(acquis)* — IP + masque donnés → bloc/quotient/reste/validité en 30 secondes. Sert d'échauffement, pas de nouvel apprentissage.
- **B. VLSM à l'envers** *(en cours)* — nombre d'hôtes voulu → trouver le masque (/n et décimal). Un succès autonome (400 hôtes → /23), à consolider par répétition.
  - *Exercice B1 en attente* : 30 machines → quel masque (/n + décimal) ?
- **C. Découpage complet — rôle sysadmin** *(nouveau, pas encore pratiqué)* — un bloc de départ + une liste de services avec leurs besoins en hôtes → découper tout le bloc soi-même, sans chevauchement, du plus grand besoin au plus petit ("largest-first").
  - *Exercice C1 en attente* : bloc `192.168.10.0/24`, 4 services (Ventes 60, IT 25, RH 10, Salle de réunion 2) → masque, réseau, broadcast, plage utilisable pour chacun.
- **D. Dépannage (troubleshooting)** *(pas encore pratiqué hors zip)* — diagramme avec une erreur cachée à repérer par le raisonnement, dans l'esprit de NetPractice mais en variantes inventées.
- **E. Table de routage / passerelle** *(pas encore pratiqué hors zip)* — plusieurs routeurs, vérifier ou corriger une route/passerelle mal placée.
- **F. Sprint flashcards** *(pas encore pratiqué)* — "masque → bloc" en rafale, zéro contexte, pour automatiser la reconnaissance pure.
