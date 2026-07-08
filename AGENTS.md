# SOC Analyser — Contexte Agentic

## Stack technique
- **Backend** : Python 3.12+ / FastAPI / SQLAlchemy 2.0 / Pydantic v2 / SQLite
- **Frontend** : Vanilla JS / Tailwind CSS (CDN) / HTML single-page
- **Docker** : Image multi-stage python:3.12-slim + Nginx, Docker Compose
- **Tests** : pytest + httpx (TestClient)

## Architecture backend

```
projet/backend/app/
```

- `main.py` — App FastAPI, CORS, inclusion des routers
- `config.py` — Variables d'environnement
- `database.py` — SQLAlchemy engine, session, Base
- `models.py` — 6 modèles : Scan, Host, Service, CVE, Technique, BruteForceResult
- `schemas.py` — Pydantic request/response schemas

### routers/
- `soc/scans.py` — CRUD scans, stats, exports, import, autobrute
- `soc/bruteforce.py` — Hydra brute force
- `redteam/labs.py` — Lab vulnérable, SQLi proxy, SSH brute force

### services/
- `nmap_service.py` — subprocess nmap + parsing XML
- `cve_service.py` — matching service → CVE (base locale + NVD API optionnelle)
- `mitre_service.py` — mapping CVE → MITRE ATT&CK
- `hydra_service.py` — subprocess hydra SSH
- `export_service.py` — CSV/JSON export
- `docker_service.py` — subprocess docker (build/run/inspect/stop)

### data/
- `cve_data.py` — Base locale de CVE (structurée par service/version)
- `mitre_data.py` — Base locale de techniques MITRE (par CVE)

## Architecture frontend

```
projet/frontend/
```

- `index.html` — SPA mono-page (SOC + Red Team)
- `app.js` — Routage, polling, appels API, animations
- `style.css` — Tailwind + custom (badges, bar-chart, progress, terminal, responsive)

## Règles pour tous les agents

### Code
- Pas de commentaires superflus dans le code (le code doit être auto-documenté)
- Suivre les conventions existantes (nommage, structure, imports)
- Les imports relatifs utilisent `.` et `..` selon la profondeur du package
- Toujours garder la compatibilité avec Python 3.12+
- Toujours passer par `get_db` pour les sessions DB (sauf background tasks qui créent leur propre `SessionLocal`)

### Données
- Les CVE et MITRE sont embarquées dans `app/data/` — pas de dépendance externe obligatoire
- Format CVE : `{cve_id, cvss_score, severity (critical/high/medium/low), description}`
- Format MITRE : `{technique_id, tactic, name, description}` — une CVE peut avoir plusieurs techniques

### Frontend
- Pas de bibliothèque JS externe (hors Tailwind CDN)
- SPA sans routage URL — sections cachées/montrées via `showSection()`
- API appelée via `apiFetch()` (wrapper autour de fetch)
- Les données temps réel utilisent le polling (setInterval 3s)
- Les couleurs suivent le thème dark (bg-gray-900, text-gray-100)

### Tests
- Base de données SQLite in-memory pour les tests
- `conftest.py` mock `app.routers.soc.scans.run_nmap_scan` pour éviter les vrais scans
- Toujours lancer `python -m pytest projet/backend/tests/ -v` avant de finaliser
- Les tests fonctionnels doivent couvrir les parcours utilisateur complets
- Les tests de non-régression doivent passer avant chaque commit

## Workflow agentic

### Scrum Master (agent primaire)
- Analyse les demandes et les traduit en user stories
- Décompose en sprints dans `gestion-projet/sprints.md`
- Met à jour `gestion-projet/backlog.md`
- Coordonne les sous-agents (fullstack-developer, tester, devops)
- Valide les livrables

### Fullstack Developer (subagent)
- Implémente les fonctionnalités backend et frontend
- Respecte la séparation SOC/Red Team dans les routers
- Crée les fichiers dans les dossiers appropriés
- Signale les dépendances entre tâches

### Tester (subagent)
- Écrit les tests unitaires, d'intégration et fonctionnels
- Lance les tests en boucle jusqu'à 100% de réussite
- Vérifie la non-régression sur l'ensemble des tests existants
- Reporte les échecs et leurs causes

### DevOps (subagent)
- Gère le versioning (Git) : branches, commits, tags, releases
- Gère les pipelines CI/CD (GitHub Actions) : workflows, runs, diagnostics
- Interagit avec GitHub via `gh` CLI (PRs, issues, releases)
- Respecte la stratégie de branching : `main` → `dev` → `feature/*`

## Décisions d'architecture clés
- **Base unique** : Une seule image Docker avec backend (uvicorn) + frontend (Nginx)
- **Lab vulnérable** : Conteneur séparé `vuln-web-server` avec PHP + MySQL + SSH
- **Séparation SOC/Red Team** : Onglets frontend distincts, routers backend séparés dans `routers/soc/` et `routers/redteam/`
- **Pas de WebSocket** : Le polling (setInterval 3s) suffit pour les mises à jour temps réel
- **Outils natifs** : nmap, hydra
- **GitHub CLI** : Les agents Scrum Master et DevOps utilisent `gh` (GitHub CLI) et `git` pour la gestion de projet, le versioning et les pipelines
- **Token GitHub** : Un `GITHUB_TOKEN` est requis dans `.env` (scopes : repo, project, workflow). Variables `author` et `email` aussi définies dans `.env.example`.
- **Avant toute commande `gh`**, exécute `set -a; source .env 2>/dev/null; set +a` pour charger le token GitHub dans l'environnement.
