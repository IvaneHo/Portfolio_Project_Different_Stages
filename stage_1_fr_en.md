# Stage 1 — Idea Development / Développement de l’idée

[🇫🇷 Français](#-version-française) · [🇬🇧 English](#-english-version)

---

## 🇫🇷 Version Française

> **Titre provisoire du projet :** TrueNAS Mobile\
> **Auteur :** Ivane Bagashvili (Holberton School)\
> **Date :** *18 au 29-08‑2025*

---

### 0) Formation de l’équipe (Team Formation)

**Composition :** projet mené en solo (ouvert à 1–2 collaborateurs si besoin).\
**Rôles (RACI, même en solo) :**

- **Product Owner (Accountable)** — vision, périmètre, critères d’acceptation : *Ivane*.
- **Mobile Engineer (Responsible)** — dev Flutter/Dart, intégration UI/UX, CI/CD : *Ivane*.
- **API Integrator (Responsible)** — appels REST TrueNAS, sécurité (token, certificats) : *Ivane*.
- **QA/Release (Consulted)** — plan de test, assets Play Store, versioning : *Ivane*.

**Normes & collaboration :**

- Mini‑daily asynchrone (hier/aujourd’hui/blocages) loggé sur le Kanban.
- Git : `main` (stable), `dev` (intégration), branches `feat/*`, PR + review.
- Definition of Done : compile, tests OK, lint clean, docs/README à jour, démo enregistrée.
- Outils : GitHub (repo + Projects), Android Studio + Flutter, Postman, Notion/Docs.

**Mon rôle & outils :** développement Flutter, intégration TrueNAS (Dio), sécurité (secure storage + biométrie), qualité (tests/CI). Organisation via **Kanban** GitHub Projects (TODO/Doing/Done), issues liées aux commits, releases taguées.

---

### 1) Recherche & Brainstorming

**Méthodes :** Mind Mapping, SCAMPER, “How Might We…”, scan concurrentiel (stores / forums TrueNAS & self‑hosted).\
**Preuves (artefacts conseillés)** : photo d’un mind map, liste brute d’idées, croquis Crazy‑8s.

---

### 2) Idées initiales (concepts explorés & rejetés)

1. **MiniPortfolios** — générateur instantané de portfolio/CV.\
   **Rejeté** : marché saturé, différenciation coûteuse en marketing, monétisation difficile sans audience.
2. **ProofEasy** — attestations d’activité (heures/tâches → PDF signé).\
   **Rejeté** : chevauchement avec des SaaS existants, nuances légales selon pays.
3. **ErgoFix** — micro‑coach posture/poignet (rappels + routines).\
   **Rejeté** : nécessite capteurs/validation biomécanique, cycles d’itération longs.
4. **Assistant “Jarvis” (ASR/NLP)** — assistant vocal généraliste.\
   **Rejeté** : forte complexité (wake‑word, STT/NLU, dialogue), dépendances ML/stat, périmètre MVP trop large.

---

### 3) Évaluation des idées (Idea Evaluation)

**Critères pondérés :** Impact/Besoin 25%, Faisabilité 20%, Time‑to‑MVP 20%, Monétisation 20%, Différenciation 10%, Apprentissage 5%.

**Matrice de décision (1–5, plus grand = meilleur) :**

| Idée               | Impact | Faisabilité | Temps | Monétisation | Différenciation | Apprentissage | **Total pondéré** |
| ------------------ | ------ | ----------- | ----- | ------------ | --------------- | ------------- | ----------------- |
| **TrueNAS Mobile** | 5      | 4           | 4     | 4            | 4               | 4             | **4.25**          |
| MiniPortfolios     | 3      | 5           | 4     | 3            | 3               | 3             | 3.60              |
| ProofEasy          | 4      | 4           | 4     | 4            | 3               | 3             | 3.85              |
| ErgoFix            | 3      | 3           | 3     | 3            | 4               | 4             | 3.15              |
| LegalLite          | 4      | 3           | 3     | 4            | 3               | 3             | 3.45              |
| SoundBlock         | 3      | 3           | 3     | 3            | 4               | 4             | 3.15              |
| Assistant “Jarvis” | 4      | 2           | 1     | 2            | 4               | 5             | 2.65              |

**Risques/Contraintes par idée :** marché, conformité, matériel, dette technique, temps d’intégration.

---

### 4) Décision & affinage (Decision and Refinement)

**Pourquoi *************************TrueNAS Mobile************************* est retenue :**

- **Niche sous‑servie** (self‑hosters TrueNAS) avec douleur réelle (contrôler/monitorer vite sans UI desktop).
- **Viabilité technique** : API REST TrueNAS v2 stable, LAN en MVP, extensions futures (Tailscale/Cloudflare Tunnel).
- **Sécurité** : stockage chiffré, biométrie, bonnes pratiques réseau.
- **Monétisation** : Pro (notifications SMART/temp, multi‑serveurs, widgets, WebDAV, relay d’accès distant).
- **Fit compétences** : Flutter, REST, CI/CD, architecture clean — démontrable et vendable.

#### Problème à résoudre (Problem Statement)

**Problème central :** sur mobile, les utilisateurs TrueNAS n’ont pas un moyen rapide, sécurisé et ergonomique pour consulter l’état du serveur et (dés)activer des services sans passer par l’interface Web desktop.

**Douleurs actuelles :**

- Trop d’étapes : ouvrir un navigateur, saisir l’IP, se connecter, naviguer dans plusieurs menus.
- Interface Web peu optimisée mobile ; actions simples lentes (10–60 s).
- Pas d’accès LAN pratique avec **stockage de token chiffré** + **biométrie**.
- Pas de retour instantané en cas de problème (p. ex. service down, surchauffe) — *(couvert en post‑MVP via notifications).*

**Solution MVP :**

- Application mobile dédiée avec **login par token chiffré** + **verrouillage biométrique**.
- **Dashboard instantané** (CPU/RAM/uptime) et **bascule ON/OFF** des services courants.

**Critères de succès (MVP) :**

- Temps pour voir l’état du NAS **≤ 2 s** en LAN après ouverture.
- Bascule d’un service en **≤ 3 taps**, confirmation claire, état persistant.
- **≥ 80 %** des testeurs jugent l’app **plus rapide** que l’UI Web pour les tâches courantes.
  **Utilisateurs cibles :** home‑lab & self‑hosted, TPE/équipes utilisant TrueNAS.\
  **Résultats attendus (MVP) :** login sécurisé, dashboard clair, services ON/OFF fiables.

---

### 5) MVP — Description & Stack

- **Résumé :** appli Flutter sécurisée pour monitorer/contrôler un TrueNAS en LAN (auth token, stockage chiffré, dashboard, services).
- **Challenges :** certificats auto‑signés, UX d’erreurs, tests.

**Stack MVP (dès l’étape 1) :**

- **Langage :** Dart · **Framework :** Flutter (Material 3, dark par défaut) · **Android min SDK :** 24
- **Navigation :** go\_router · **État :** flutter\_riverpod · **HTTP :** Dio
- **Modèles/JSON :** Freezed + json\_serializable
- **Stockage sécurisé :** flutter\_secure\_storage (Keystore/Keychain)
- **Biométrie :** local\_auth
- **Cache local (optionnel) :** Isar (reco) / Hive ; SQL : sqflite/drift
- **API :** TrueNAS v2.0 (REST/JSON)
- **CI/CD :** GitHub Actions · **Qualité :** flutter\_lints, flutter\_test, mocktail

---

### 6) Processus & Documentation

- **Idées considérées** : forces/faiblesses/raisons de rejet documentées.
- **Synthèse MVP** : impact attendu, risques, métriques de succès.
- **Traçabilité** : Kanban GitHub Projects, issues ↔ commits/PR, changelog par release.

---

### 7) Plan & Jalons

- **S1 — Specs & squelette** : wireframes, contrats de données, thèmes M3, navigation (GoRouter), état (Riverpod), Mock API.
- **S2 — Cœur MVP** : login + secure storage, dashboard, services ON/OFF, tests contrôleurs, lint/CI.
- **S3 — Polish & démo** : erreurs, loaders, biométrie, README, vidéo de démo, retours testeurs.
- **(Stretch) S4** : vue read‑only disques/datasets.

---

### 8) Risques & Atténuation

- **Certificats auto‑signés / réseau** : HttpClient natif + doc options sûres (cert fiable, tunnel sécurisé).
- **Scope creep** : backlog priorisé, MVP strict, feature flags.
- **Conformité monétisation** : anticiper Google Play Billing si Pro.
- **Charge dev solo** : tâches courtes, automatisation CI.

---

### 9) Technologies & Outils (stack détaillé)

**App** : Flutter/Dart, Material 3, go\_router, Riverpod, Dio (interceptors), Freezed/JSON, secure storage, local\_auth, Isar/Hive.\
**Plus tard** : FCM (notifications), WebDAV (fichiers), Tailscale/CF Tunnel (accès distant), relay (SaaS).\
**Projet** : GitHub repo + Projects (Kanban), GitHub Actions, flutter\_lints/tests, mocktail, README/Notion.

---

### 10) Annexes

**User stories**

- En tant que propriétaire de NAS, je stocke URL/token en sécurité pour éviter la ressaisie.
- En tant qu’utilisateur, je vois CPU/RAM/uptime sur un seul écran.
- En tant qu’utilisateur, je (dés)active SMB/NFS/SSH rapidement.

**Critères d’acceptation (MVP)**

- URL/token valides → redirection Dashboard après login.
- Pull‑to‑refresh → mise à jour < 2 s en LAN pour CPU/RAM/uptime.
- Bascule SMB → état persistant après refresh.
- Token invalide → message clair, on reste sur la connexion.

---

## 🇬🇧 English Version

> **Working title:** TrueNAS Mobile\
> **Author:** Ivane Bagashvili (Holberton School)\
> **Date:** *2025*‑08‑18 to 29 

---

### 0) Team Formation

**Setup:** solo project (open to adding 1–2 collaborators).\
**Roles (RACI even when solo):**

- **Product Owner (Accountable)** — vision, scope, acceptance criteria: *Ivane*.
- **Mobile Engineer (Responsible)** — Flutter/Dart dev, UI/UX integration, CI/CD: *Ivane*.
- **API Integrator (Responsible)** — TrueNAS REST calls, security (token, certs): *Ivane*.
- **QA/Release (Consulted)** — test plan, Play Store assets, versioning: *Ivane*.

**Working agreements:**

- Async micro‑standup (yesterday/today/blockers) logged on Kanban.
- Git: `main` (stable), `dev` (integration), `feat/*` branches, PR + review.
- Definition of Done: compiles, tests pass, lint clean, docs updated, demo recorded.
- Tools: GitHub repo + Projects, Android Studio + Flutter, Postman, Notion/Docs.

**My role & tooling:** Flutter development, TrueNAS integration (Dio), security (secure storage + biometrics), quality (tests/CI). Organised via **GitHub Projects Kanban** (TODO/Doing/Done), issues linked to commits, tagged releases.

---

### 1) Research & Brainstorming

**Methods:** Mind Mapping, SCAMPER, “How Might We…”, competitive scan (stores / TrueNAS & self‑hosted forums).\
**Evidence (recommended artefacts):** mind map photo, raw ideas list, Crazy‑8s sketches.

---

### 2) Initial Ideas (explored & rejected)

1. **MiniPortfolios** — instant portfolio/CV generator.\
   **Rejected:** saturated market, costly differentiation, weak monetization without audience.
2. **ProofEasy** — weekly activity attestations (hours/tasks → signed PDF).\
   **Rejected:** overlaps with existing SaaS, country‑specific legal nuances.
3. **ErgoFix** — posture/wrist micro‑coach (reminders + routines).\
   **Rejected:** needs sensors/biomech validation, longer iteration cycles.
4. **“Jarvis” assistant (ASR/NLP)** — general voice assistant.\
   **Rejected:** high complexity (wake‑word, STT/NLU, dialogue), ML/stat dependencies, MVP too broad for the timeline.

---

### 3) Idea Evaluation

**Weighted criteria:** Impact/Need 25%, Feasibility 20%, Time‑to‑MVP 20%, Monetization 20%, Differentiation 10%, Learning 5%.

**Decision matrix (1–5, higher is better):**

| Idea               | Impact | Feasibility | Time | Monetization | Differentiation | Learning | **Weighted Total** |
| ------------------ | ------ | ----------- | ---- | ------------ | --------------- | -------- | ------------------ |
| **TrueNAS Mobile** | 5      | 4           | 4    | 4            | 4               | 4        | **4.25**           |
| MiniPortfolios     | 3      | 5           | 4    | 3            | 3               | 3        | 3.60               |
| ProofEasy          | 4      | 4           | 4    | 4            | 3               | 3        | 3.85               |
| ErgoFix            | 3      | 3           | 3    | 3            | 4               | 4        | 3.15               |
| LegalLite          | 4      | 3           | 3    | 4            | 3               | 3        | 3.45               |
| SoundBlock         | 3      | 3           | 3    | 3            | 4               | 4        | 3.15               |
| “Jarvis” assistant | 4      | 2           | 1    | 2            | 4               | 5        | 2.65               |

**Risks/constraints per idea:** market, compliance, hardware, tech debt, integration time.

---

### 4) Decision & Refinement

**Why *************************TrueNAS Mobile************************* was retained:**

- **Underserved niche** (TrueNAS self‑hosters) with a clear pain: quick control/monitoring without the desktop UI.
- **Direct technical viability:** stable TrueNAS v2 REST API, LAN for MVP, future extensions (Tailscale/Cloudflare Tunnel).
- **Security fit:** encrypted storage, biometrics, sane networking practices.
- **Monetization path:** Pro features (SMART/temp notifications, multi‑server, widgets, WebDAV, remote relay).
- **Skill alignment:** Flutter, REST, CI/CD, clean architecture — demo‑able and sellable.

#### Problem Statement

**Core problem:** On mobile, TrueNAS users lack a fast, secure, and ergonomic way to check server health and toggle services without using the desktop‑focused Web UI.

**Current pain points:**

- Too many steps: open browser, type IP, sign in, navigate multiple menus.
- Web UI is not mobile‑optimized; basic actions are slow (10–60 s).
- No convenient LAN access with **encrypted token storage** + **biometrics**.
- No instant feedback/alerts when issues occur — *(post‑MVP via notifications).*

**MVP solution:**

- Dedicated mobile app with **encrypted token login** + **biometric lock**.
- **Instant dashboard** (CPU/RAM/uptime) and **one‑tap ON/OFF** for core services.

**MVP success criteria:**

- Time‑to‑status **≤ 2 s** on LAN after app open.
- Toggle a service in **≤ 3 taps**, with clear confirmation and persistent state.
- **≥ 80%** of testers report the app is **faster** than the Web UI for common tasks.
  **Target users:** home‑lab/self‑hosted users, small teams using TrueNAS.\
  **Expected outcomes (MVP):** secure login, clear dashboard, reliable ON/OFF service control.

---

### 5) MVP — Description & Stack

- **Summary:** secure Flutter app to monitor/control a TrueNAS over LAN (token auth, encrypted storage, dashboard, services).
- **Challenges:** self‑signed certificates, error UX, tests.

**MVP stack (Stage 1):**

- **Language:** Dart · **Framework:** Flutter (Material 3, dark by default) · **Android min SDK:** 24
- **Navigation:** go\_router · **State:** flutter\_riverpod · **HTTP:** Dio
- **Models/JSON:** Freezed + json\_serializable
- **Secure storage:** flutter\_secure\_storage (Keystore/Keychain)
- **Biometrics:** local\_auth
- **Local cache (optional):** Isar (recommended) / Hive; SQL: sqflite/drift
- **API:** TrueNAS v2.0 (REST/JSON)
- **CI/CD:** GitHub Actions · **Quality:** flutter\_lints, flutter\_test, mocktail

---

### 6) Process & Documentation

- **Ideas considered:** documented strengths/weaknesses/rejection reasons.
- **MVP summary:** expected impact, risks, success metrics.
- **Traceability:** GitHub Projects Kanban, issues ↔ commits/PR, release changelog.

---

### 7) Plan & Milestones

- **W1 — Specs & skeleton:** wireframes, data contracts, M3 themes, navigation (GoRouter), state (Riverpod), Mock API.
- **W2 — Core MVP:** login + secure storage, dashboard, services ON/OFF, controller tests, lint/CI.
- **W3 — Polish & demo:** error states, loaders, biometrics, README, demo video, tester feedback.
- **(Stretch) W4:** read‑only disks/datasets view.

---

### 8) Risks & Mitigation

- **Self‑signed certs / networking:** native HttpClient + safe options (valid cert or secure tunnels).
- **Scope creep:** prioritized backlog, strict MVP, feature flags.
- **Monetization compliance:** plan Play Billing early if Pro.
- **Solo dev load:** small tasks, CI automation.

---

### 9) Technologies & Tools (detailed stack)

**App:** Flutter/Dart, Material 3, go\_router, Riverpod, Dio (interceptors), Freezed/JSON, secure storage, local\_auth, Isar/Hive.\
**Later:** FCM (notifications), WebDAV (files), Tailscale/CF Tunnel (remote), relay (SaaS).\
**Project:** GitHub repo + Projects (Kanban), GitHub Actions, flutter\_lints/tests, mocktail, README/Notion.

---

### 10) Appendices

**User stories**

- As a NAS owner, I securely store URL/token to avoid re‑entry.
- As a user, I see CPU/RAM/uptime on one screen.
- As a user, I quickly (de)activate SMB/NFS/SSH.

**Acceptance criteria (MVP)**

- Valid URL/token → redirect to Dashboard after login.
- Pull‑to‑refresh → updates < 2s on LAN for CPU/RAM/uptime.
- Toggling SMB → state persists after refresh.
- Invalid token → clear error, remain on login.

