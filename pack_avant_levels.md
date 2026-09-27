# Pack avant les levels — 7 exos, puis tu fonces

## Pourquoi le subnetting existe (en une minute)

Une seule grande adresse IP pour tout le monde poserait deux problèmes : (1) gaspillage énorme — une entreprise avec 10 machines n'a pas besoin d'un bloc de 65 000 adresses ; (2) tout le monde serait sur le même domaine de broadcast — chaque message "à tous" atteindrait des milliers de machines qui n'en ont rien à faire. Le subnetting découpe un grand bloc en morceaux de la bonne taille, un par salle/service/segment physique. C'est tout — pas plus mystique que ça.

## Comment utiliser ce pack

Fais les 7. Vérifie avec le corrigé en bas. **6/7 ou plus → tu passes direct aux levels, sans repasser par moi.** En dessous de 6, redemande-moi juste ceux qui coincent (pas une reprise complète). Rappel formule si besoin : `bloc = 256 - octet du masque = 2^(32-n)`.

---

### Exercice 1 — Réseau/broadcast/plage (nouveau préfixe)
**Pourquoi celui-là** : tu as fait `/26` et `/28`, jamais `/27` — vérifier que la méthode généralise, pas juste que tu as mémorisé un cas.
`10.4.7.130/27` → réseau, broadcast, plage utilisable ?

### Exercice 2 — Même réseau ? (cas piège : proches en apparence)
**Pourquoi celui-là** : c'est *exactement* le test que Level 2 te demande entre deux hosts reliés directement.
`172.20.5.10/28` et `172.20.5.30/28` sont-ils sur le même réseau ?

### Exercice 3 — Même réseau ? (cas piège inverse : loin en apparence)
**Pourquoi celui-là** : pour te forcer à calculer au lieu de juger "à l'œil" — deux nombres éloignés peuvent être dans le même bloc.
`192.168.9.5/26` et `192.168.9.60/26` sont-ils sur le même réseau ?

### Exercice 4 — Corriger un masque cassé
**Pourquoi celui-là** : c'est le mécanisme exact d'un des deux hosts du Level 2 — masque éditable, à toi de le déduire pour que ça matche l'autre host.
`10.0.0.65/27` est correct et fixe. Un deuxième host, sur le même lien, a l'IP fixée à `10.0.0.70` mais son masque affiché est `/24` (donc faux). Quel masque doit-il avoir pour être sur le même réseau que le premier ?

### Exercice 5 — Compléter une IP manquante
**Pourquoi celui-là** : le mécanisme miroir de l'exo 4 — masque fixe, IP à choisir dans la bonne plage.
`192.168.4.9/29` est fixe. Un deuxième host doit être sur le même réseau, masque `/29` imposé. Donne le réseau concerné et une IP valide possible pour ce deuxième host.

### Exercice 6 — Lien point-à-point (/30)
**Pourquoi celui-là** : c'est la deuxième paire du Level 2 (deux routeurs reliés directement) — un `/30` n'a que 2 adresses utilisables, pas de marge d'erreur.
Un routeur a `192.168.100.9/30`. Quelle est la seule adresse possible pour l'appareil en face sur ce même lien ?

### Exercice 7 — Réseaux différents : qu'est-ce qu'il manque ?
**Pourquoi celui-là** : pont vers ce que les levels suivants vont creuser (routes, passerelle) — juste le déclic conceptuel, pas le calcul complet.
`192.168.1.10/24` veut joindre `192.168.2.10/24`. Même réseau ? Si non, qu'est-ce qu'il faut configurer côté premier host, et quel appareil rend la connexion possible ?

---
## méthode:
```txt
Le récapitulatif final — méthode + pourquoi

1. Trouver le bloc : bloc = 256 - octet_masque = 2^(32-n)
Pourquoi : le bloc, c'est la taille de chaque tranche du réseau — combien d'adresses consécutives forment un sous-réseau.

2. Trouver l'octet coupé : le premier octet du masque qui n'est ni 0 ni 255 (raccourci : compte les octets à 255 pleins, le suivant est le bon).
Pourquoi : avant cet octet, tout est "100% réseau" (masque = 255, doit matcher exactement). Après, tout est "100% hôte" (masque = 0, ignoré pour la comparaison). Seul l'octet coupé est un mélange des deux — c'est le seul endroit où il faut calculer.

3. Diviser cet octet par le bloc → quotient et reste.
Pourquoi : le quotient te dit dans quelle tranche (quel sous-réseau) tu tombes ; le reste te dit où exactement tu es à l'intérieur de cette tranche.

4. Adresse réseau = quotient × bloc sur l'octet coupé ; tout ce qui est avant reste identique, tout ce qui est après devient 0.
Pourquoi : le réseau, c'est la première adresse du bloc — tous les bits "hôte" à 0.

5. Broadcast = réseau + bloc - 1 sur l'octet coupé ; tout ce qui est après devient 255.
Pourquoi : le broadcast, c'est la dernière adresse du bloc — tous les bits "hôte" à 1.

6. Même réseau, deux hôtes ? → les octets avant l'octet coupé doivent être identiques ET les deux quotients (sur l'octet coupé) doivent être égaux.
Pourquoi : c'est facile d'oublier la première condition quand on ne travaille que sur le 4ème octet (elle est automatiquement vraie). Avec /20, /18 etc., deux hôtes peuvent avoir le même quotient sur l'octet coupé mais un octet différent avant — et là, ce n'est PAS le même réseau.

7. Une adresse est-elle valide ? → reste = 0 → c'est l'adresse réseau (invalide). reste = bloc-1 → c'est le broadcast (invalide). Sinon → hôte valide.
Pourquoi : le réseau et le broadcast servent à désigner le bloc lui-même, jamais une machine.
```
## Corrigé

1. Bloc 32 (`/27`, masque `.224`). `130` tombe dans le bloc `128–159` → **réseau 10.4.7.128, broadcast 10.4.7.159, plage .129–.158**.
2. Bloc 16 (`/28`). `10` → bloc `0–15` (réseau `.0`). `30` → bloc `16–31` (réseau `.16`). **Réseaux différents → PAS le même réseau.**
3. Bloc 64 (`/26`). `5` → bloc `0–63`. `60` → aussi bloc `0–63` (60 < 64). **Même réseau (.0).**
4. Bloc 32 (`/27`). `65` → bloc `64–95` (réseau `.64`). `70` est aussi dans `64–95`. Avec `/24`, le deuxième host se retrouverait sur le réseau `10.0.0.0` — incohérent. **Il doit avoir `/27` (255.255.255.224)** pour partager le réseau `.64`.
5. Bloc 8 (`/29`). `9` → bloc `8–15` → **réseau 192.168.4.8**, broadcast `.15`, plage `.9–.14`. IP valide pour le deuxième host : n'importe laquelle parmi `.10, .11, .12, .13, .14` (pas `.9` déjà pris, pas `.8` ni `.15`).
6. Bloc 4 (`/30`). `9` → bloc `8–11` → réseau `.8`, broadcast `.11`, seulement 2 adresses utilisables : `.9` et `.10`. Le premier routeur a `.9`, donc **l'autre doit être `.10`**.
7. `192.168.1.0` ≠ `192.168.2.0` → **réseaux différents**. Le premier host a besoin d'une **passerelle par défaut** configurée (une interface d'un routeur sur son propre réseau), et il faut un **routeur** avec une interface sur chacun des deux réseaux pour faire réellement passer les paquets de l'un à l'autre.
