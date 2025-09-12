# Stage 2 — Project Charter / Charte de projet  
*Version 1.0 — 2025-09-12*  

[🇬🇧 English](#english) · [🇫🇷 Français](#fr)  

---

## English — Project Charter {#english}

### 1. Project Objectives (Purpose + SMART goals)

**Purpose**  
The project aims to provide a fast and secure mobile experience to check the status of a TrueNAS server and toggle essential services, without relying on the desktop Web UI.  

**Background**  
During Stage 1, ideation combined mind mapping and the SCAMPER method (Substitute, Combine, Adapt, Modify, Put to use, Eliminate, Reverse). This approach identified quick wins such as one-tap service toggles and token-based login.  

**SMART objectives (MVP)**  
The application should display the server status in less than two seconds on a LAN connection after opening. It must include secure login with token and biometrics, never store secrets in plaintext, and cover authentication and error handling through tests. Service control for SMB, NFS and SSH must be possible in no more than three taps, with a success rate of at least 99 percent using the TrueNAS v2 API.  

---

### 2. Stakeholders and Roles  

| Stakeholder                                | Interest                | Role / RACI                                        |
| ------------------------------------------ | ----------------------- | -------------------------------------------------- |
| Ivane Bagashvili                           | Deliver a usable MVP    | **R/A** dev & scope; **C** testing/release         |
| Holberton instructors                      | Review & grading        | **C** checkpoints; **I** progress                  |
| Early testers (home-lab / small teams)     | Usability & reliability | **C** feedback; **I** fixes                        |
| Future and current NAS owners              | Adoption                | **C** expectations; **I** roadmap                  |
| TrueNAS docs/community                     | API reference           | **I** only                                         |

R = Responsible, A = Accountable, C = Consulted, I = Informed  

Communication will take place through a short weekly status note and a demo GIF. Issues and decisions will be tracked in GitHub using a list view.  

---

### 3. Scope  

The MVP includes support for a single TrueNAS server, secure token storage in Keychain/Keystore, and a dashboard showing CPU, RAM and uptime with pull-to-refresh. Users can enable or disable SMB, NFS and SSH services with clear confirmations. Basic settings allow configuration of the server URL, the token and biometric lock.  

The MVP does not cover multi-server support, notifications such as SMART or temperature alerts, file-browser writes (read-only may be added later via WebDAV), remote tunnels (Tailscale or Cloudflare), ZFS or dataset management, backups or snapshots, or any voice assistant and orchestration features.  

The project assumes LAN usage only, with a single TrueNAS server and access to the v2 REST API. The first platform is Android (minimum SDK 24). Devices must support biometrics, and the token is pre-created by an administrator. Remote tunnels, multi-server features and ZFS management are excluded from the MVP.  

---

### 4. Risks and Mitigation  

| Risk                                  | Mitigation                                                                 |
| ------------------------------------- | -------------------------------------------------------------------------- |
| Self-signed certificates / LAN quirks | Safe paths with a valid certificate or secure tunnel, controlled HTTP client, and clear error messages |
| API differences / breaking changes    | Target TrueNAS v2, wrap calls in a service layer, and run endpoint smoke tests |
| Solo-developer bandwidth              | Small tasks, continuous integration, strict MVP scope, weekly reviews      |
| Security regressions                  | Secure storage and biometrics, no plaintext tokens, authentication tests, and a review checklist |
| Store compliance (if Pro later)       | Early review of policies, optional telemetry with proper documentation     |

Dependencies include the availability of the TrueNAS v2 API, stable local network access, the use of the Android Keystore/Keychain for secure storage, and the participation of testers for usability sessions.  

---

### 5. High-Level Plan  

| Stage                          | Dates                       | Key deliverables                                                      |
| ------------------------------ | --------------------------- | --------------------------------------------------------------------- |
| Stage 1 — Idea Development     | 2025-08-18 → 2025-08-29     | Stage 1 report approved                                               |
| Stage 2 — Project Charter      | 2025-09-01 → 2025-09-12     | Charter finalized                                                     |
| Stage 3 — Technical Docs       | 2025-09-15 → 2025-09-26     | API contracts, error model, screen map and wireframes                 |
| Stage 4 — MVP Development      | 2025-09-29 → 2025-10-24     | Login and secure storage → dashboard → service toggles → polish/tests |
| Stage 5 — Closure              | 2025-10-27 → 2025-11-07     | Demo video, tester feedback, README, optional beta                    |

---

## Français — Charte de projet {#fr}

### 1. Objectifs (But + SMART)

**But**  
L’objectif est de fournir sur smartphone une expérience rapide et sécurisée permettant de consulter l’état d’un TrueNAS et d’activer ou de désactiver ses services clés, sans passer par l’interface Web desktop.  

**Contexte**  
Lors de l’étape 1, l’idéation a combiné le mind map et la méthode SCAMPER (Substituer, Combiner, Adapter, Modifier, Détourner, Éliminer, Inverser). Cette approche a mis en évidence des gains rapides comme les interrupteurs à un seul geste et la connexion par token.  

**Objectifs SMART (MVP)**  
L’application doit afficher l’état du serveur en moins ou égal à deux secondes sur LAN après ouverture. Elle doit proposer une connexion sécurisée via token et biométrie, ne jamais stocker de secrets en clair, et inclure des tests sur les parcours d’authentification et d’erreur. Le contrôle des services SMB, NFS et SSH doit être possible en trois tapes maximum avec un taux de réussite d’au moins 99 % sur l’API TrueNAS v2.  

---

### 2. Parties prenantes et rôles  

| Partie prenante                           | Intérêt             | Rôle / RACI                                   |
| ----------------------------------------- | ------------------- | --------------------------------------------- |
| Ivane Bagashvili                          | Livrer un MVP utile | **R/A** dev & périmètre ; **C** tests/release |
| Encadrants Holberton                      | Suivi & évaluation  | **C** jalons ; **I** avancement               |
| Testeurs (home-lab / petites équipes)     | Retours d’usage     | **C** sessions ; **I** correctifs             |
| Futurs / actuels propriétaires de NAS     | Adoption            | **C** attentes ; **I** feuille de route       |
| Docs / communauté TrueNAS                 | Référence API       | **I** uniquement                              |

R = Responsable, A = Approbateur, C = Consulté, I = Informé  

La communication passera par une note hebdomadaire et une mini démo GIF. Le suivi des issues et décisions sera effectué sur GitHub.  

---

### 3. Périmètre  

Le MVP inclut un serveur TrueNAS, le stockage sécurisé du token (Keychain/Keystore), un tableau de bord avec CPU, RAM et uptime et la fonction pull-to-refresh. Il permet d’activer ou de désactiver SMB, NFS et SSH avec confirmation. Les réglages de base intègrent l’URL du serveur, le token et la biométrie.  

Ne sont pas inclus : le multi-serveurs, les notifications comme SMART ou température, l’écriture dans l’explorateur/WebDAV (la lecture seule pourra être ajoutée plus tard), les tunnels distants tels que Tailscale ou Cloudflare, la gestion ZFS ou des datasets, les sauvegardes ou snapshots et les assistants vocaux ou d’orchestration.  

Les hypothèses et contraintes sont les suivantes : usage limité au LAN, un seul serveur, API v2 uniquement, Android en premier (SDK minimum 24), appareil doté de la biométrie et token créé en amont par un administrateur. Aucun tunnel distant, multi-serveur ou gestion ZFS n’est prévu pour le MVP.  

---

### 4. Risques et atténuation  

| Risque                                   | Atténuation                                                                   |
| ---------------------------------------- | ----------------------------------------------------------------------------- |
| Certificats auto-signés / réseau domest. | Parcours sûrs avec certificat valide ou tunnel, client HTTP contrôlé, UX claire |
| Écarts ou ruptures d’API                 | Cibler TrueNAS v2, passer par une couche service, effectuer des tests « smoke » |
| Charge d’un dev solo                     | Découper en petites tâches, CI, périmètre strict, revue hebdomadaire          |
| Régressions sécurité                     | Stockage sécurisé et biométrie, aucun token en clair, tests d’auth, checklist |
| Conformité store (si Pro)                | Lecture des politiques en amont, télémétrie optionnelle et documentée         |

Les dépendances concernent la disponibilité de l’API TrueNAS v2, l’accès au réseau local, le Keystore/Keychain Android et la disponibilité des testeurs.  

---

### 5. Plan haut niveau  

| Étape                        | Dates                         | Livrables clés                                                              |
| ---------------------------- | ----------------------------- | --------------------------------------------------------------------------- |
| Étape 1 — Dév. de l’idée     | 18 → 29 août 2025             | Rapport validé                                                              |
| Étape 2 — Charte             | 1 → 12 septembre 2025         | Charte finalisée                                                            |
| Étape 3 — Docs techniques    | 15 → 26 septembre 2025        | Contrats API, modèle d’erreurs, plan d’écrans et wireframes                 |
| Étape 4 — Dév. MVP           | 29 septembre → 24 octobre 25  | Login et stockage sécurisé → dashboard → ON/OFF services → tests et finitions |
| Étape 5 — Clôture            | 27 octobre → 7 novembre 2025  | Vidéo démo, rapport testeurs, README, bêta éventuelle                       |
