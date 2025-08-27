# Stage 1 — Idea Development / Développement de l’idée

[🇬🇧 English](#-english-version) · [🇫🇷 Français](#-version-française)

---

## 🇬🇧 English Version

> **Working title:** TrueNAS Mobile
> **Author:** Ivane Bagashvili (Holberton School)
> **Date:** *2025-08-18 to 2025-08-29*

---

### 0) Team Formation

This is a **solo project**. I act as Product Owner (define the need and acceptance criteria), Mobile Engineer (Flutter app), API Integrator (TrueNAS REST), and QA/Release (test plan and release assets).

**Working style:** a short daily check‑in note at 09:00 (yesterday / today / blockers). Git workflow: `main` (stable), `dev` (integration), feature branches `feat/...`, merge via pull request to keep history clean. **Definition of Done:** builds on device and emulator, unit tests pass, lints clean, README updated (with a short demo video when possible). **Tools:** GitHub Issues/Projects (list view), Android Studio + Flutter, Postman for endpoints, a Notion/Docs page for decisions.

---

### 1) Research & Brainstorming

Starting point: on **mobile**, the TrueNAS Web UI is slow and awkward. I listed pain points, drew a quick mind map and Crazy‑8s sketches, and scanned existing apps and TrueNAS/self‑hosted forums. Several ideas emerged; two were attractive but too large for the timeline (see below). **TrueNAS Mobile** was the fastest path to something useful.

---

### 2) Initial Ideas (explored & rejected)

**Multi‑NAS/Cloud backup orchestrator.** One app to schedule backups across ZFS/BTRFS/SMB/S3. **Rejected:** very high cross‑platform complexity, critical restore paths, data‑loss risk; too big for an MVP.

**“Jarvis” assistant (ASR/NLP).** General‑purpose voice assistant (wake word, STT/NLU, dialog). **Rejected:** heavy ML stack, latency/privacy concerns, and a long integration time.

---

### 3) Idea Evaluation

Weighted criteria: Impact/Need 25%, Feasibility 20%, Time‑to‑MVP 20%, Monetization 20%, Differentiation 10%, Learning 5%.

| Idea                                | Impact | Feasibility | Time | Monetization | Differentiation | Learning | **Weighted Total** |
| ----------------------------------- | :----: | :---------: | :--: | :----------: | :-------------: | :------: | :----------------: |
| **TrueNAS Mobile**                  |    5   |      4      |   4  |       4      |        4        |     4    |      **4.25**      |
| Multi‑NAS/Cloud backup orchestrator |    4   |      2      |   2  |       3      |        4        |     4    |        3.00        |
| “Jarvis” assistant                  |    4   |      2      |   1  |       2      |        4        |     5    |        2.65        |

Reading: **TrueNAS Mobile** balances value, risk, and speed. The other two have good potential but exceed MVP scope.

---

### 4) Decision & Refinement

Why **TrueNAS Mobile** was retained: clear mobile need (check status and toggle a service in seconds), direct feasibility with TrueNAS v2 REST over LAN, and an obvious roadmap (notifications, multi‑server, WebDAV file browser, remote access via Tailscale/Cloudflare Tunnel).

**Problem statement:** too many steps on mobile, no secure token storage + biometrics, no quick alerts (planned post‑MVP).

**MVP solution:** dedicated app with encrypted‑token login and biometric lock, instant dashboard (CPU/RAM/uptime), and reliable ON/OFF switches for core services.

**Success (MVP):** status visible ≤ **2 s** after app open; a service toggled in ≤ **3 taps** with clear confirmation; ≥ **80%** of test users find it faster than the Web UI.

---

### 5) MVP — Description & Stack

The MVP focuses on three things and does them well: secure **connection** (URL/IP + token), fast **dashboard** (CPU, RAM, uptime), and **service control** (SMB, NFS, SSH) with clear errors.

Stack: Flutter/Dart (Material 3), go\_router (navigation), Riverpod (state), Dio (HTTP), Freezed + json\_serializable (models), flutter\_secure\_storage (encrypted secrets), local\_auth (biometrics), optional Isar (local cache), TrueNAS API v2 (REST/JSON), GitHub Actions (lint/tests/builds).

---

### 6) Process & Documentation

Ideas documented with reasons; MVP goals/risks/success metrics; traceability via GitHub Issues/Projects (list view), links issues ↔ commits/PR, and a release changelog.

---

### 7) Plan & Milestones

Week 1: wireframes, data contracts, theme, navigation/state, Mock API. Week 2: login + secure storage, dashboard, ON/OFF services, basic tests, lint/CI. Week 3: polished errors/loaders, biometrics, README, demo video and tester feedback. Optional Week 4: read‑only disks/datasets.

---

### 8) Risks & Mitigation

Self‑signed certs and home‑network quirks handled by safe paths (valid cert or secure tunnel) and controlled HTTP client behavior; scope creep kept in check with a prioritized backlog and MVP discipline; plan Play Billing early if Pro.

---

### 9) Technologies & Tools (detailed stack)

App: Flutter/Dart, Material 3, go\_router, Riverpod, Dio (interceptors), Freezed/JSON, secure storage, local\_auth, Isar/Hive. Later: FCM notifications, WebDAV files, Tailscale/Cloudflare Tunnel, possible relay SaaS. Project: GitHub repo + Projects (list view), GitHub Actions, flutter\_lints/tests, mocktail, README/Notion.

---

### 10) Appendices

User stories: store URL/token securely to avoid re‑entry; see CPU/RAM/uptime on one screen; quickly (de)activate SMB/NFS/SSH.
Acceptance (MVP): valid URL/token redirects to Dashboard; pull‑to‑refresh updates status < 2 s on LAN; toggled service state persists after refresh; invalid token shows a clear error and keeps the user on login.

---

## 🇫🇷 Version Française

> **Titre provisoire du projet :** TrueNAS Mobile
> **Auteur :** Ivane Bagashvili (Holberton School)
> **Date :** *18–29 août 2025*

---

### 0) Formation de l’équipe (Team Formation)

Je mène le projet en solo pour l’instant. Concrètement, j’endosse à la fois le rôle de “product owner” (je clarifie le besoin et les critères d’acceptation) et celui de développeur mobile/integ API (je code l’app Flutter, je branche l’API TrueNAS, je prépare les builds). Pour rester carré, je garde aussi un petit chapeau “QA/Release” : un plan de tests simple et les éléments de publication.

Côté organisation, je reste pragmatique : un court message chaque matin à 09:00 dans une note de suivi (hier / aujourd’hui / blocages). Dans Git, je travaille avec `main` (stable), `dev` (intégration) et des branches `feat/<sujet>`. Je ne merge qu’avec une PR, même en solo, pour garder l’historique propre. Ma “Definition of Done” tient en quatre points : l’app compile sur mon téléphone et l’émulateur, les tests unitaires des contrôleurs passent, le lint est propre, et le README est à jour (avec une courte capture vidéo si possible).

Outils : un dépôt GitHub (ex. `github.com/<user>/truenas-mobile`) avec suivi des tâches via GitHub **Issues** et **Projects** (vue liste), Android Studio + Flutter pour le dev, **Postman** pour valider les endpoints TrueNAS, et une note Notion/Google Docs pour les décisions.

---

### 1) Recherche & Brainstorming

Je suis parti de mon usage quotidien : quand je veux juste vérifier le NAS depuis le canapé, l’interface Web n’est pas agréable sur téléphone et ça prend trop de clics. J’ai listé ces irritations, puis j’ai fait un rapide mind map et quelques croquis (Crazy‑8s) pour tester différentes pistes. J’ai aussi regardé ce qui existe sur les stores et sur les forums TrueNAS/self‑hosted pour voir où une petite app pouvait réellement aider. De là, plusieurs idées sont sorties, dont deux “grosses” que j’ai finalement écartées (voir ci‑dessous), et TrueNAS Mobile qui restait la plus simple à rendre utile vite.

---

### 2) Idées initiales (concepts explorés & rejetés)

Au démarrage, deux pistes fortes ont été étudiées puis écartées pour des raisons de périmètre et de risque.

**Orchestrateur de sauvegardes multi‑NAS/Cloud.** L’idée consistait à piloter depuis une application unique des plans de sauvegarde vers plusieurs cibles hétérogènes (ZFS/BTRFS/SMB/S3). Si la proposition de valeur est élevée pour des environnements complexes, la réalité technique l’est tout autant : interopérabilité multi‑fournisseurs, scénarios de restauration critiques, risques de perte de données et exigence d’une traçabilité irréprochable. L’effort d’ingénierie et de validation dépasse largement ce qu’un MVP académique peut absorber. Cette idée a donc été classée « hors‑scope » pour l’instant.

**Assistant « Jarvis » (ASR/NLP).** L’ambition ici était de proposer un assistant vocal généraliste (détection de mot‑clé, reconnaissance vocale, compréhension du langage, gestion de dialogue et actions). Malgré un fort potentiel d’expérience utilisateur, la chaîne technologique requise (STT/NLU on‑device ou cloud, modèles ML, latence, confidentialité) impose une complexité et un temps d’intégration incompatibles avec les contraintes du projet. L’idée est mise en réserve pour une exploration ultérieure, possiblement avec un périmètre beaucoup plus restreint.

---

### 3) Évaluation des idées (Idea Evaluation)

Afin d’objectiver le choix, une grille pondérée a été utilisée. Elle met l’accent sur l’impact utilisateur et la rapidité d’atteindre un MVP fonctionnel, sans négliger la faisabilité et la monétisation. La matrice ci‑dessous synthétise le scoring.

**Matrice de décision (1–5, plus grand = meilleur) :**

| Idée                          | Impact | Faisabilité | Temps | Monétisation | Différenciation | Apprentissage | **Total pondéré** |
| ----------------------------- | :----: | :---------: | :---: | :----------: | :-------------: | :-----------: | :---------------: |
| **TrueNAS Mobile**            |    5   |      4      |   4   |       4      |        4        |       4       |      **4.25**     |
| Orchestrateur multi‑NAS/Cloud |    4   |      2      |   2   |       3      |        4        |       4       |        3.00       |
| Assistant “Jarvis”            |    4   |      2      |   1   |       2      |        4        |       5       |        2.65       |

La lecture de cette matrice montre que **TrueNAS Mobile** offre le meilleur compromis entre valeur, risque et délai. L’orchestrateur multi‑NAS/Cloud souffre d’une complexité intrinsèque élevée, tandis que l’assistant vocal pâtit d’un time‑to‑MVP trop long. Ces éléments confirment la pertinence d’un démarrage par un produit ciblé, livrable rapidement et extensible.

---

### 4) Décision & affinage

J’ai choisi **TrueNAS Mobile** parce qu’elle répond à un besoin très concret : sur mobile, je veux voir l’état du serveur et activer/désactiver un service en quelques secondes, sans galérer dans l’UI Web. Techniquement, c’est aussi celle que je peux livrer rapidement : l’API REST v2 de TrueNAS est documentée et testable facilement sur le réseau local. Le périmètre du MVP est volontairement petit (connexion avec token chiffré, un tableau de bord clair, la liste des services avec un interrupteur) pour tenir le délai tout en offrant une vraie valeur. Les extensions à moyen terme sont déjà évidentes : notifications (SMART/températures), multi‑serveurs, explorateur de fichiers via WebDAV, et un accès distant guidé (Tailscale/Cloudflare Tunnel).

---

### 5) MVP — Description & Stack

Le MVP fait trois choses, mais il les fait bien : il se connecte à un serveur TrueNAS avec un token que je garde chiffré sur l’appareil ; il affiche tout de suite CPU, RAM et uptime ; et il me laisse activer/désactiver les services essentiels (SMB, NFS, SSH) sans naviguer dans dix écrans. Je n’essaie pas de tout couvrir au début : je préfère une base solide, rapide et sûre.

Côté technique, je reste sobre : **Flutter/Dart**, **Material 3** pour le look, **go\_router** pour la navigation, **Riverpod** pour l’état. **Dio** gère les requêtes et **Freezed/json\_serializable** les modèles. Le token et l’URL sont dans **flutter\_secure\_storage**, avec **local\_auth** pour le verrouillage biométrique. Si besoin d’un peu d’hors‑ligne, **Isar** fera un cache léger. L’API ciblée est **TrueNAS v2 (REST/JSON)**. Je mets une petite chaîne **GitHub Actions** pour lancer lint, tests et builds.

---

### 6) Processus & Documentation

* **Idées considérées** : forces/faiblesses/raisons de rejet documentées.
* **Synthèse MVP** : impact attendu, risques, métriques de succès.
* **Traçabilité** : GitHub Issues/Projects (vue liste), issues ↔ commits/PR, changelog par release.

---

### 7) Plan & Jalons

Je découpe en semaines pour rester lisible. La première semaine, je pose le squelette : écrans, navigation, état, thème et une fausse API pour développer sans dépendre d’un NAS. La deuxième, je fais le cœur : l’écran de connexion (avec stockage sécurisé), le dashboard et les services ON/OFF avec des messages d’erreur clairs. La troisième, je peaufine : gestion des états de chargement et des erreurs, ajout de la biométrie, README propre et une courte vidéo de démo pour Holberton. Si j’ai de la marge, j’ajoute une vue en lecture seule des disques et datasets.

---

### 8) Risques & Atténuation

Le sujet sensible, c’est la gestion des certificats auto‑signés et, plus largement, les aléas réseau à la maison. Je documente des chemins sûrs (certificat valide quand c’est possible, ou tunnel type Tailscale/Cloudflare) et je contrôle le comportement du client HTTP pour éviter les mauvaises surprises. L’autre piège, c’est l’emballement du périmètre : je garde un backlog avec des priorités et je m’interdis d’ajouter une feature si elle ne sert pas la démo MVP. Enfin, pour la publication avec une version Pro, j’anticipe la facturation Google Play pour ne pas tout découvrir au dernier moment.

---

### 9) Technologies & Outils (stack détaillé)

**App** : Flutter/Dart, Material 3, go\_router, Riverpod, Dio (interceptors), Freezed/JSON, secure storage, local\_auth, Isar/Hive.
**Plus tard** : FCM (notifications), WebDAV (fichiers), Tailscale/CF Tunnel (accès distant), relay (SaaS).
**Projet** : GitHub repo + Projects (vue liste), GitHub Actions, flutter\_lints/tests, mocktail, README/Notion.

---

### 10) Annexes

**User stories**

* En tant que propriétaire de NAS, je stocke URL/token en sécurité pour éviter la ressaisie.
* En tant qu’utilisateur, je vois CPU/RAM/uptime sur un seul écran.
* En tant qu’utilisateur, je (dés)active SMB/NFS/SSH rapidement.

**Critères d’acceptation (MVP)**

* URL/token valides → redirection Dashboard après login.
* Pull‑to‑refresh → mise à jour < 2 s en LAN pour CPU/RAM/uptime.
* Bascule SMB → état persistant après refresh.
* Token invalide → message clair, on reste sur la connexion.
