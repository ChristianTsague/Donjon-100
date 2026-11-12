# 🏰 Donjon-100

> **100 salles, un donjon.** Chaque salle est un mini-projet pratique en systèmes,
> réseaux et cybersécurité. Je les franchis un par un, en public, en apprenant
> en produisant. Bienvenue dans ma partie.
> vous retrouverez le catalogue complet des 100 salles juste en haut

![Progression](https://img.shields.io/badge/Donjon-1%2F100_salles_franchies-red)
![Focus](https://img.shields.io/badge/Stack-Linux_%7C_R%C3%A9seaux_%7C_Cybers%C3%A9curit%C3%A9-blue)

---

## 🧭 La règle du jeu

- **1 TP = 1 salle = 1 dossier.** À l'intérieur : les artefacts réels du projet
  (documentations, scripts, captures, configurations).
- **Apprendre en produisant** : chaque salle laisse derrière elle un livrable
  consultable, pas juste des notes.
- **100% légal** : tous les tests se font sur mon propre matériel, mon propre
  réseau, ou avec autorisation écrite.
- **En public** : erreurs comprises, pas seulement les réussites. C'est là
  qu'on apprend vraiment.

## ⚔️ L'équipement
   Outil | Rôle |
 |-------|------|
 | Pop!_OS | Poste principal et serveur de labo |
 | Termux (Android) | Station technique mobile, client SSH |
 | Docker & VMs | Terrains de jeu isolés |
 | Wazuh, Suricata, Cowrie, Wireshark, pfSense | L'arsenal de détection et de réseau |

## 🗺️ La carte du donjon

### Module 1 — Fondations (TP 01-10)
 | #  | Salle | Thème | Statut |
 |--- |-------|-------|--------|
 | 01 | [Termux & SSH](TP-01-termux-ssh/) | Téléphone → station technique | ✅ |
 | 02 | Chasseur d'échecs SSH | Détection de bruteforce | 🔲 |
 | 03 | L'œil du réseau | Wireshark, TCP/IP | 🔲 |
 | 04 | Le mur | pfSense, DMZ | 🔲 |
 | 05 | [Le piège](https://github.com/ChristianTsague/HONEYPOD-SIEM) | Honeypot Cowrie | ✅ |
 | 06 | [La tour de guet](https://github.com/ChristianTsague/HONEYPOD-SIEM) | SOC : Wazuh + Suricata | ✅ |
 | 07 | Premier C | Scanner de ports en C | 🔲 |
 | 08 | Mini-shell | Programmation système | 🔲 |
 | 09 | Le chat botté | Réponse automatisée | 🔲 |
 | 10 | Maître du donjon | Box vulnérable communautaire | 🔲 |

### Module 2 — La station mobile (TP 11-20)
 | #  | Salle | Thème | Statut |
 |--- |-------|-------|--------|
 | 11 | Know Thy Machine | Téléphone → station technique |🔲 |
 | 12 | Cartographe de Poche | Scan de réseau (nmap) | 🔲 |
 | 13 | L'Inventaire | Inventaire des services | 🔲 |
 | 14 | Clés en Main | Durcissement SSH| 🔲 |
 | 15 | Serveur de Poche| Serveur web local | 🔲|
 | 16 | Col Porter | Transferts de fichiers | 🔲 |
 | 17 | Vigie Distant | Supervision à distance | 🔲 |
 | 18 | Trafic Mobile| Analyse du trafic du téléphone | 🔲 |
 | 19 | [Le Censeur](https://github.com/ChristianTsague/DHCP-DNS) | DNS BIND9 avec filtrage | ✅ |
 | 20 | [Le Duel des Passerelles](https://github.com/ChristianTsague/Relay-DHCP) | Conflit DHCP volontaire | ✅ |

### Module 3 — Détection et SOC niveau 2 (TP 21-30)

 | #  | Salle | Thème | Statut |
 |--- |-------|-------|--------|
 | 21 | Anti-Recon | Détection de scan nmap (Suricata) |🔲 |
 | 22 | Python Prêtre | Parsing de logs en Python | 🔲 |
 | 23 | Corrélateur | Détection d'attaque en 2 étapes | 🔲 |
 | 24 | Tableau de Bord | Dashboard Grafana | 🔲 |
 | 25 | Le Rapporteur| Rapports automatiques (cron) | 🔲|
 | 26 | Sirène de Poche | Bot Telegram d'alerte | 🔲 |
 | 27 | Honeytoken | Fichier appât + auditd | 🔲 |
 | 28 | Canari DNS| Domaine piège DNS | 🔲 |
 | 29 | Chronologiste | Frise chronologique d'attaque | 🔲 |
 | 30 | Purple Rain | Exercice offensif ↔ défensif | 🔲 |


### Module 4 — C système et bas niveau (TP 31-40)

 | #  | Salle | Thème | Statut |
 |--- |-------|-------|--------|
 | 31 | Traqueur de Mémoire | Fuites mémoire (malloc/free)|🔲 |
 | 32 | Pile ou Face | Pile vs tas (stack/heap) | 🔲 |
 | 33 | Overflow Volontaire| Buffer overflow observé (gdb) | 🔲 |
 | 34 | Les Boucliers | Protections (ASLR, canary, NX)| 🔲 |
 | 35 | Mini-Netcat| Réimplémenter netcat en C | 🔲|
 | 36 | Moulinette à Logs | Traitement de logs en C | 🔲 |
 | 37 | Casseur Éthique | Cassage de hash (éthique) | 🔲 |
 | 38 | Canari DNS| Format ELF, compilation| 🔲 |
 | 39 | Shellcode 101| Comprendre le shellcode | 🔲 |
 | 40 | Détecteur en Boîte | Bibliothèque de détection | 🔲 |

 ### Module 5 — Web : comprendre en cassant le sien (TP 41-50)

| # | Salle | Thème | Statut |
|---|-------|-------|--------|
| 41 | Site de Cristal | Site vulnérable volontaire | 🔲 |
| 42 | L'Intercepteur | Manipulation de requêtes (ZAP) | 🔲 |
| 43 | Injection Contrôlée | SQLi sur son propre site | 🔲 |
| 44 | Script mal Placé | XSS | 🔲 |
| 45 | L'Escalier Raté | IDOR / accès non autorisés | 🔲 |
| 46 | Canon à Pâte | Fuzzing de chemins | 🔲 |
| 47 | Le Voleur de Clics | CSRF | 🔲 |
| 48 | La Blindée | Durcissement du site | 🔲 |
| 49 | Cryptophile | Hachage : md5 vs bcrypt | 🔲 |
| 50 | L'Audit du Siècle | Audit complet de son site | 🔲 |

### Module 6 — Pentest labo 100% légal (TP 51-60)

| # | Salle | Thème | Statut |
|---|-------|-------|--------|
| 51 | Le Terrain de Jeu | Labo de pentest (VMs) | 🔲 |
| 52 | Détective Passif | OSINT sur soi-même | 🔲 |
| 53 | Recon de Poche | Énumération depuis Termux | 🔲 |
| 54 | Brise-Porte | Attaque SSH + fail2ban | 🔲 |
| 55 | L'Ascension | Élévation de privilèges | 🔲 |
| 56 | Château Active Directory | AD + GPO | 🔲 |
| 57 | Œil sur le Domaine | Audit Active Directory | 🔲 |
| 58 | Radio Audit | Audit Wi-Fi | 🔲 |
| 59 | La Persistance (Propre) | Techniques de persistance | 🔲 |
| 60 | Le Rapport du Pentesteur | Rapport professionnel | 🔲 |

### Module 7 — Automatisation, conteneurs et cloud (TP 61-70)

| # | Salle | Thème | Statut |
|---|-------|-------|--------|
| 61 | Général Durcisseur | Ansible | 🔲 |
| 62 | Boîte Noire | Docker Compose (SOC d'un coup) | 🔲 |
| 63 | Conteneur sous Verrous | Sécurité Docker | 🔲 |
| 64 | L'Usine | CI/CD | 🔲 |
| 65 | Le Porte-Parole | HTTPS + certificats | 🔲 |
| 66 | Premier VPS | Service en ligne (vrai monde) | 🔲 |
| 67 | Coffre-Fort | Sauvegardes + restauration | 🔲 |
| 68 | Sentinelle Extérieure | Monitoring externe | 🔲 |
| 69 | Tunnel Privé | VPN WireGuard | 🔲 |
| 70 | Secrets Bien Gardés | Zéro secret dans les repos | 🔲 |

### Module 8 — Outils pour la communauté (TP 71-80)

| # | Salle | Thème | Statut |
|---|-------|-------|--------|
| 71 | La Sentinelle a une API | API Wazuh | 🔲 |
| 72 | Écran Radar | Page d'alertes en direct | 🔲 |
| 73 | Générateur de Passe | Outil de mots de passe | 🔲 |
| 74 | Le Coffre du Citoyen | Coffre-fort chiffré | 🔲 |
| 75 | Nmap en Joli | Interface web de scan | 🔲 |
| 76 | Couteau Suisse | Boîte à outils unifiée | 🔲 |
| 77 | Le Modèle | Template de write-up | 🔲 |
| 78 | La Vitrine | Site GitHub Pages | 🔲 |
| 79 | Le Flash Info | Bulletin de veille hebdo | 🔲 |
| 80 | Traducteur Technique | Guides vulgarisés | 🔲 |

### Module 9 — Forensique et investigation (TP 81-90)

| # | Salle | Thème | Statut |
|---|-------|-------|--------|
| 81 | Histoire d'un Shell | Analyse de logs de session | 🔲 |
| 82 | Fantôme de Disque | Récupération de fichiers | 🔲 |
| 83 | Frise du Crime | Timeline multi-sources | 🔲 |
| 84 | Photographie de Mémoire | Analyse mémoire (dump) | 🔲 |
| 85 | Le PDF Piégé (Simulé) | Analyse de PDF malveillant | 🔲 |
| 86 | Autopsie d'un Phishing | Analyse de phishing | 🔲 |
| 87 | Le Chasseur de Motifs | Règles YARA | 🔲 |
| 88 | Script Malsain | Rétro-ingénierie de script | 🔲 |
| 89 | Kill Chain Appliquée | Kill chain ↔ défenses | 🔲 |
| 90 | Le Procès | Rapport forensique complet | 🔲 |

### Module 10 — Consécration (TP 91-100)

| # | Salle | Thème | Statut |
|---|-------|-------|--------|
| 91 | Donjon n°2 : le Retour | Box vulnérable communautaire | 🔲 |
| 92 | Maître de Cérémonie | Mini-CTF organisé | 🔲 |
| 93 | 100 Jours de Sécurité | Série de contenu (30 épisodes) | 🔲 |
| 94 | Passe le Relais | Mentorat (3 write-ups déclenchés) | 🔲 |
| 95 | Usine Sécurisée | Pipeline avec sécurité intégrée | 🔲 |
| 96 | Première Mission Réelle | Première mission (autorisée) | 🔲 |
| 97 | Le Grand Œuvre | Documentation type DSI | 🔲 |
| 98 | La Grande Piscine | Préparation Piscine 42 | 🔲 |
| 99 | Le Dossier | Portfolio employabilité | 🔲 |
| 100 | Le Bilan du Siècle | Bilan + certification | 🔲 |

## 📈 Progression

**Salles franchies : 5 / 100**

`▓▓░░░░░░░░░░░░░░░░░░░ 5%`

## 📮 Me suivre

- Communauté : **Cyberkid237**
- Ce dépôt est mon journal de progression. Chaque salle franchie y laisse
  une trace documentée.
