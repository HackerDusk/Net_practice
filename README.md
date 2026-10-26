_This project has been created as part of the 42 curriculum by srandro._

# Net_practice

## Table of Contents

- [Description](#description)
- [Instructions](#instructions)
  - [Run the training interface](#run-the-training-interface)
  - [Work on a level](#work-on-a-level)
  - [Export the configurations](#export-the-configurations)
  - [Submission](#submission)
- [Resources](#resources)
  - [AI usage](#ai-usage)
- [Quick calculation reminder](#quick-calculation-reminder)
  - [Definitions](#definitions-read-first)
  - [Method](#method)

## Description

NetPractice is a hands-on introduction to computer networking. The project consists of **10 levels** played in a browser-based training interface that simulates small networks (hosts, routers, switches and the Internet). Each level starts with a broken network and one or more goals, for example "host A must communicate with host B" or "host C must reach the Internet".

The goal is to fix the configuration (IP addresses, subnet masks, default gateways and routing tables) until every goal succeeds, both on the forward way and on the reverse way. The networks are simulated and are not real networks.

Through the 10 levels, the project practices:

- IPv4 addressing: network address, broadcast address and valid host addresses
- Subnet masks, CIDR notation and subnetting (block size, splitting a larger block into smaller subnets)
- Default gateways, default routes and specific routes in a routing table
- The role of routers (connect networks) and switches (connect machines inside one network)
- Reading the simulator's logs to diagnose why a packet does not arrive

## Instructions

### Run the training interface

1. Download the archive attached to the project page and extract it in any folder.
2. In this folder, run the launcher:

   ```bash
   ./run.sh
   ```

   It starts a local web server and opens the default browser on the training page.
3. If `run.sh` does not work, start the server manually and open the page yourself:

   ```bash
   python3 -m http.server 49242
   # then open http://localhost:49242 in the browser (the port can be changed)
   ```
4. In the **Training** tab, enter your intranet login and click **Start!**. The **Evaluation** tab generates a random configuration, like the one used during the defense.

### Work on a level

- Edit the unshaded fields (IP, mask, routes). Shaded fields are fixed by the level.
- Click **Check again** to test the configuration. The **logs** at the bottom of the page explain why a goal fails.
- When every goal is OK, a **Next level** button appears.

### Export the configurations
- Before leaving a level, click **Get my config** if you want to download its configuration file.

### Submission
10 exported configuration files (one per level, generated with the **Get my config** button) must be placed at the root of the repository. The login must be entered in the training interface before exporting, otherwise the files will not be valid for the defense.

## Resources
Networking concepts studied: TCP/IP addressing, subnet masks, default gateways, routers and switches, OSI layers.
- [`Learn everything by practice on networksim.app (I love this one)`](https://networksim.app/)
- [What is the Internet? Computer networks](https://youtu.be/JqweQE6TDTc?si=YUSM_-i7HTAc4-Hk)
- [What is a computer peripheral, and why is it important?](https://www.lenovo.com/fr/fr/glossary/computer-peripheral/?orgRef=https%253A%252F%252Fwww.google.com%252F)
- List of key vocabularies:
    - [Host](https://developer.mozilla.org/fr/docs/Glossary/Host)
    - Client:
        - [doc1](https://kxs.fr/cours/ihm-web/client-serveur-requete)
        - [doc2](https://fr.wikipedia.org/wiki/Client_(informatique))
    - Server:
        - [doc1](https://www.ionos.fr/digitalguide/serveur/know-how/quest-ce-quun-serveur-une-notion-deux-definitions/)
        - [doc2](https://www.hpe.com/emea_africa/fr/what-is/servers.html)
    - [Internet](https://ccn.unistra.fr/websites/ccn/documentation/Guides-Kits/Mailo_Internet_v1_1_fr.pdf)
- means of communication:
- Types of Network - PAN, LAN, WAN and MAN - classifies a network primarily according to its extent or range:
   - [All at once](https://www.geeksforgeeks.org/computer-networks/types-of-area-networks-lan-man-and-wan/)
   - [PAN](https://www.techtarget.com/enterprise-software/definition/What-is-a-personal-area-network-PAN)
   - LAN:
        - [definition](https://www.scribd.com/document/892187706/introduction-aux-reseaux-LAN)
        - [About LAN](https://itmag.tdsynnex.fr/Lexique/lan-definition-fonctionnement-et-avantages-dun-reseau-local/)
        - Router:
            - [What is a router ?](https://www.cloudflare.com/fr-fr/learning/network-layer/what-is-a-router/)
            - [Router 3D model](https://sketchfab.com/3d-models/router-archer-tp-link-ax23-41ff5f5fe0774f43a5896e33ecbe7ad0)
        - Network Switch:
            - [What is a network switch?](https://talice.com/actualites/quest-ce-quun-switch)
            - [switch 3D model](https://sketchfab.com/3d-models/network-switch-974f1aa182fc4bb1b996310e32234448)
        - Ethernet Cable Connector (RJ45):
            - [What is ethernet ?](https://www.net-usb.com/fr/usb-over-ethernet-system/what-is-ethernet/)
            - [What is an ethernet cable](https://ascentoptics.com/blog/fr/rj-45-cable/)
            - [Ethernet Cable Connector (RJ45) 3D model](https://sketchfab.com/3d-models/ethernet-cable-connector-rj45-325672cf996e472abaed009b5ca21cfc)
        - Wi-Fi:
            - [What is Wi-Fi?](https://www.geeksforgeeks.org/computer-networks/basics-of-wi-fi/)
            - [radio waves](https://sherpas.com/blog/ondes-radio/)
            - [IEEE 802.11 norm](https://fr.wikipedia.org/wiki/IEEE_802.11)
            - [the box, the modem, the router, and the Wi-Fi access point](https://pro.orange.fr/lemag/box-modem-routeur-borne-quel-equipement-choisir-pour-mon-activite-CNT000002aALa0.html)
            - Network Interface Card (NIC):
                - [modem 3D model](https://sketchfab.com/3d-models/simple-modem-8ef942f9125a4e09978021ec190cca4e)
                - [What is a Network Interface Card?](https://web.maths.unsw.edu.au/~lafaye/CCM/pc/carte-reseau.htm)
                - [NIC 3D model](https://sketchfab.com/3d-models/network-interface-card-191c8ad40de2430980b879615aa0d2e3)
            - IP Address:
                - [definition](https://www.formip.com/pages/blog/adresse-ip)
                - Subnetting:
                    - [What is subnetting?](https://www.ionos.fr/digitalguide/serveur/know-how/subnetting-comment-fonctionnent-les-sous-reseaux/)
                    - Understanding IP addresses and subnets:
                        - [DevSecOps](https://blog.stephane-robert.info/docs/reseaux/fondamentaux/ip-sous-reseaux/)
                        - [calculat.io](https://calculat.io/en/number/bin-to-dec)
                        - [Magic Number and Binary Calculation!](https://youtu.be/SMW3enlScT8?si=x-7MFmnhC-gohJNX)
                        - [ionos.fr](https://www.ionos.fr/digitalguide/serveur/know-how/subnetting-comment-fonctionnent-les-sous-reseaux/)
            - [Subnet Mask – Complete Guide](https://www.formip.com/pages/blog/masque-de-sous-reseau)
            - [magic number methode](https://youtu.be/SMW3enlScT8?si=8Cp5P6TnjeQgfOKV)
            - [FLSM & VLSM](https://ipcisco.com/lesson/vlsm-subnetting/)
            - [IPv4 Subnetting Cheat Sheet (CIDR, Mask & Special IP Ranges)](https://ipcisco.com/subnetting-cheat-sheet/)
            - MAC Address:
                - What is a MAC address?:
                    - [doc1](https://www.formip.com/pages/blog/adresse-mac)
                    - [doc2](https://windscribe.com/fr/knowledge-base/articles/what-is-mac-spoofing-and-how-to-use-it)
                - [MAC Address vs. IP Address: What’s the difference?](https://www.formip.com/pages/blog/adresse-mac)
            - [Routing: how packets find their way](https://blog.stephane-robert.info/docs/reseaux/fondamentaux/routage/#la-passerelle-gateway--la-sortie-de-votre-r%C3%A9seau)
            - [How to configure the default gateway](https://www.tp-link.com/fr-ca/support/faq/1126/)
            - [default routes](https://www.ibm.com/docs/fr/i/7.5.0?topic=concepts-default-routes)
            - [What is a default gateway?](https://protonvpn.com/fr/blog/default-gateway)
            - What is a routing table?:
                - [doc1](https://www.coursera.org/fr-FR/articles/routing-table)
                - [doc2](https://blog.stephane-robert.info/docs/cloud/architecture/03-tables-routage-et-gateways/)
            - [Debugging a network outage like a pro: a checklist of steps to follow](https://www.wildcodeschool.com/blog/d%C3%A9boguer-une-panne-r%C3%A9seau-comme-un-pro-checklist-des-%C3%A9tapes-%C3%A0-suivre)
            - [DHCP protocol](https://learn.microsoft.com/fr-fr/windows-server/networking/technologies/dhcp/dhcp-top)
            - [ARP protocol](https://www.fortinet.com/fr/resources/cyberglossary/what-is-arp)
            - [What is a domain name ?](https://www.one2net.fr/nom-domaine/qu-est-ce-qu-un-nom-de-domaine/)
            - [What is the DNS protocol?](https://www.ibm.com/fr-fr/think/topics/dns-protocol)
            - [TCP/IP Addressing](https://www.avast.com/fr-fr/c-what-is-tcp-ip)
            - [What is UDP?](https://www.fortinet.com/fr/resources/cyberglossary/user-datagram-protocol-udp)
            - [The 14 essential protocols(HTTP/HTTPS and so on)](https://www.lemagit.fr/conseil/Reseau-comprendre-les-14-protocoles-essentiels)
    - [MAN](https://www.edrawsoft.com/fr/article/man-network-diagram.html)
    - WAN:
        - [LAN vs WAN]:
            - [doc1](https://www.scribd.com/document/909426972/LES-COMPOSANTS-DES-RESEAUX-LAN-ET-WAN)
            - [doc2](https://www.lafibrelyonnaise.fr/lan-vs-wan)
    - [successive Euclidean divisions review](https://www.logamaths.fr/pgcd-divisions-euclidiennes-successives-algorithme-d-euclide/)
- [The Best Way To Learn Networking](https://www.youtube.com/watch?v=OBqCYxhwR_o)
- OSI Model:
    - [What is the OSI model?](https://www.ionos.fr/digitalguide/serveur/know-how/le-modele-osi-reference-pour-les-standards/)
    - [Physical layer](https://www.ionos.fr/digitalguide/serveur/know-how/couche-physique/)
    - [CRC: Definition and Uses](https://fr.wikipedia.org/wiki/Contr%C3%B4le_de_redondance_cyclique)
    - shielded cabling (STP)
        - [definition](https://www.cae-groupe.com/guide-blindage-cable)
        - [STP 3D model](https://sketchfab.com/3d-models/shielded-twisted-pair-ethernet-cable-ad9aaf30f56f4c97a95fa8fb5c6721c1)
    - [Bandwidth vs. throughput](https://www.tp-link.com/fr/blog/208/bande-passante-vs-d%C3%A9bit/)
    - [Latency](https://infofibre.fr/glossaire/latence)
    - [data link layer (MAC, switches)](https://www.ionos.fr/digitalguide/serveur/know-how/couche-liaison-de-donnees/)
    - [network layer (IP, routers)](https://www.ionos.ca/digitalguide/server/know-how/network-layer/)
    - [transport layer (TCP/UDP, ports)](https://www.ionos.ca/digitalguide/server/know-how/transport-layer/)
    - [session layer (session management)](https://www.ionos.ca/digitalguide/server/know-how/session-layer/)
    - [presentation layer (data translation, encryption, and compression)](https://www.ionos.ca/digitalguide/server/know-how/presentation-layer/)
    - [application layer (the layer the user is using)](https://www.ionos.ca/digitalguide/server/know-how/application-layer/)

### AI usage

AI was used as a learning assistant, never to solve the levels for me:

- **Finding resources**: to discover `deeper` documentation about networking concepts (subnetting, gateways, routing tables, OSI model).
- **Clarifying concepts**: to re-explain parts that were unclear in some documentations.
- **Summaries and review**: to help write short summaries of the OSI layers and to check this README against the subject requirements.

> The project was developed with a focus on understanding, experimentation, and mainly peer learning.

## Quick calculation reminder

### Definitions (read first)

- **Cut octet**: among the mask's 4 octets, the one whose value is **neither `0` nor `255`** (a mix of network bits and host bits). This is the **only** place where a calculation is needed — every other octet is compared directly, no math involved.
- **Block**: the size of one slice (the number of consecutive addresses that make up a subnet), measured only on the cut octet.
  `block = 256 − (mask value on the cut octet)`
- **Quotient**: the integer-division quotient of **(cut octet's value in the IP) ÷ block**. Tells you **which slice** (which subnet) this address falls into.
- **Remainder**: the remainder of that same division, **(cut octet's value) MOD block**. Tells you the address's **exact position** inside its slice (0 = very first, block−1 = very last).
- **Subnet**: the entire slice — every possible address in it, from the first to the last, inclusive.
- **Network address**: the **very first** address of a subnet (position 0 in the slice). Only used to **name** the subnet — never assignable to a machine.
- **Broadcast address**: the **very last** address of a subnet (last possible position). Used to send a message to **every** machine in the subnet at once — never assignable to a single machine.

### Method

| Step | Exact formula | Why |
|---|---|---|
| 1. Block | `block = 256 − mask_value_on_cut_octet` | Size of the slice this address belongs to. |
| 2. Find the cut octet | The 1st mask octet that is neither `0` nor `255` | Before it: everything is network (must match exactly). After it: everything is host (free). Only this one is mixed. |
| 3. Quotient and remainder | `quotient = cut_octet_value_in_IP ÷ block` (integer division); `remainder = cut_octet_value_in_IP MOD block` | Quotient = which slice. Remainder = which position inside that slice. |
| 4. Network address | On the cut octet: `quotient × block`. Octets before: same as the IP. Octets after: `0`. | First address of the slice = all host bits set to 0. |
| 5. Broadcast address | On the cut octet: `(quotient × block) + block − 1`. Octets before: same as the IP. Octets after: `255`. | Last address of the slice = all host bits set to 1. |
| 6. Same subnet, two hosts? | Octets **before** the cut octet identical **AND** the two quotients (on the cut octet) identical | Easy trap when only working on the 4th octet: the 1st condition is automatically true there, so it gets forgotten. With /20, /18, etc., two hosts can share the same quotient but differ in an earlier octet — that is **not** the same subnet. |
| 7. Is the address valid? | remainder `= 0` → network address (invalid). remainder `= block − 1` → broadcast (invalid). Otherwise → valid host. **This rule alone only holds when the cut octet is the LAST octet of the address.** If it isn't the last one, also check the octet(s) **after** it: they must be `0` to confirm "network", or `255` to confirm "broadcast" — otherwise a remainder of 0 or block−1 can still be a perfectly valid host address. | Network and broadcast name the slice itself, never a machine — but that identity only holds when there's nothing left to check after the cut point. |
