# Sprints - SOC Analyser

---

## Sprint 1 : Fondations du projet
**Durée : 1 semaine**
**Objectif : Mettre en place la structure du projet, l'infrastructure backend/frontend et la base de données.**

| Tâche | US | Agent | Description |
|-------|----|-------|-------------|
| 1.1 | — | fullstack-developer | Créer la structure des dossiers (backend/, frontend/, docker/) |
| 1.2 | — | fullstack-developer | Initialiser le projet FastAPI (main.py, routes, config) |
| 1.3 | — | fullstack-developer | Définir les modèles SQLite (Scan, Host, Service, CVE, Technique) avec SQLAlchemy |
| 1.4 | — | fullstack-developer | Créer les endpoints CRUD de base pour les scans |
| 1.5 | — | fullstack-developer | Initialiser le frontend avec Tailwind CSS + Vanilla JS (index.html, app.js) |
| 1.6 | — | fullstack-developer | Créer le Dockerfile multi-stage backend+frontend (Nginx) |
| 1.7 | — | tester | Tests unitaires : modèles et endpoints CRUD |
| 1.8 | — | tester | Tests d'intégration : création et consultation de scan |

**Livrables :**
- Projet structuré backend/ + frontend/
- API FastAPI opérationnelle
- Base SQLite avec migrations
- Frontend basique avec Tailwind
- Dockerfile fonctionnel

---

## Sprint 2 : Analyse réseau avec Nmap
**Durée : 1 semaine**
**Objectif : Intégrer Nmap et permettre le scan réseau depuis l'interface.**

| Tâche | US | Agent | Description |
|-------|----|-------|-------------|
| 2.1 | US1 | fullstack-developer | Intégration de python-nmap ou sous-process Nmap |
| 2.2 | US1 | fullstack-developer | API POST /scan - lancer un scan depuis une IP/plage |
| 2.3 | US2 | fullstack-developer | API POST /scan - détection des services et versions |
| 2.4 | US1 | fullstack-developer | Persistance des résultats en base de données |
| 2.5 | US1, US2 | fullstack-developer | Page frontend : formulaire de scan + affichage des résultats |
| 2.6 | US10 | fullstack-developer | Page frontend : historique des analyses |
| 2.7 | — | tester | Tests unitaires : parsing XML Nmap, sauvegarde |
| 2.8 | — | tester | Tests d'intégration : scan complet + vérification base |

**Livrables :**
- Scan réseau fonctionnel
- Détection services/versions
- Persistance en base
- Interface de scan et historique

---

## Sprint 3 : Corrélation CVE & MITRE ATT&CK
**Durée : 2 semaines**
**Objectif : Corréler les services avec des CVE et techniques MITRE ATT&CK.**

| Tâche | US | Agent | Description |
|-------|----|-------|-------------|
| 3.1 | US3 | fullstack-developer | Intégration API NVD (National Vulnerability Database) pour les CVE |
| 3.2 | US3 | fullstack-developer | Algorithme de matching service/version → CVE |
| 3.3 | US3 | fullstack-developer | Stockage des CVE en base avec score CVSS |
| 3.4 | US4 | fullstack-developer | Intégration du mapping CVE → MITRE ATT&CK |
| 3.5 | US4 | fullstack-developer | Stockage des techniques MITRE en base |
| 3.6 | US3, US4 | fullstack-developer | API GET /scan/{id}/vulns - listing des vulnérabilités |
| 3.7 | US3, US4 | fullstack-developer | Page frontend : vue détaillée des vulnérabilités avec code couleur |
| 3.8 | — | tester | Tests unitaires : matching CVE, mapping MITRE |
| 3.9 | — | tester | Tests d'intégration : scan → CVE → MITRE |

**Livrables :**
- Base de CVE locale
- Matching automatique service → CVE
- Techniques MITRE ATT&CK associées
- Interface vulnérabilités avec code couleur

---

## Sprint 4 : Rapports & Export
**Durée : 1 semaine**
**Objectif : Générer des rapports exportables en CSV et JSON.**

| Tâche | US | Agent | Description |
|-------|----|-------|-------------|
| 4.1 | US5 | fullstack-developer | Génération export CSV (hôtes, services, CVE) |
| 4.2 | US6 | fullstack-developer | Génération export JSON structuré |
| 4.3 | US5, US6 | fullstack-developer | API GET /scan/{id}/export/{format} |
| 4.4 | US5, US6 | fullstack-developer | Page frontend : boutons d'export + téléchargement |
| 4.5 | US9 | fullstack-developer | Amélioration UI : métriques détaillées sur le dashboard |
| 4.6 | — | tester | Tests unitaires : exports CSV et JSON |
| 4.7 | — | tester | Tests d'intégration : export complet d'une analyse |

**Livrables :**
- Export CSV fonctionnel
- Export JSON fonctionnel
- Dashboard avec métriques
- Téléchargement depuis l'interface

---

## Sprint 5 : Brute Force SSH & Automatisation
**Durée : 1.5 semaines**
**Objectif : Intégrer Hydra et automatiser le workflow scan → brute force.**

| Tâche | US | Agent | Description |
|-------|----|-------|-------------|
| 5.1 | US7 | fullstack-developer | Intégration Hydra (sous-process) |
| 5.2 | US7 | fullstack-developer | API POST /bruteforce - paramétrage et lancement |
| 5.3 | US7 | fullstack-developer | Affichage et persistance des résultats de brute force |
| 5.4 | US7 | fullstack-developer | Page frontend : formulaire brute force + résultats |
| 5.5 | US8 | fullstack-developer | Import fichier XML Nmap (upload) |
| 5.6 | US8 | fullstack-developer | Extraction auto des services SSH → lancement brute force |
| 5.7 | US8 | fullstack-developer | Workflow automatisé : scan → SSH détecté → brute force |
| 5.8 | — | tester | Tests unitaires : parsing XML, lancement Hydra |
| 5.9 | — | tester | Tests d'intégration : workflow automatisé complet |

**Livrables :**
- Brute force SSH via Hydra
- Import fichier XML Nmap
- Workflow automatisé scan → brute force
- Interface dédiée

---

## Sprint 6 : UI/UX, Finalisation & Tests
**Durée : 1 semaine**
**Objectif : Peaufiner l'interface, les tests et préparer la livraison.**

| Tâche | US | Agent | Description |
|-------|----|-------|-------------|
| 6.1 | US9 | fullstack-developer | Design moderne final : animations, transitions, responsive |
| 6.2 | US9 | fullstack-developer | Code couleur dangerosité : rouge (critique), orange (élevé), etc. |
| 6.3 | US9 | fullstack-developer | Widgets métriques : graphiques, compteurs, tendances |
| 6.4 | US11 | fullstack-developer | Finalisation Docker : image unique optimisée |
| 6.5 | US11 | fullstack-developer | Documentation : README, docker-compose, déploiement |
| 6.6 | — | tester | Tests unitaires : couverture maximale de toutes les couches |
| 6.7 | — | tester | Tests d'intégration : parcours utilisateur complet |
| 6.8 | — | tester | Tests de non-régression sur tous les sprints |
| 6.9 | — | tester | Rapport final de tests |

**Livrables :**
- Application complète et testée
- Docker image unique
- Documentation de déploiement
- Rapport de tests final

---

## Récapitulatif

| Sprint | Durée | Sujet |
|--------|-------|-------|
| S1 | 1 sem | Fondations (structure, FastAPI, SQLite, Tailwind, Docker) |
| S2 | 1 sem | Analyse réseau Nmap (scan IP, services, historique) |
| S3 | 2 sem | Corrélation CVE & MITRE ATT&CK |
| S4 | 1 sem | Rapports (CSV, JSON, métriques dashboard) |
| S5 | 1.5 sem | Brute force SSH Hydra + automatisation |
| S6 | 1 sem | UI/UX final, polish, tests, doc |
| S7 | — | Non réalisé (fusionné S6/S8) |
| S8 | 2 sem | Red Team & Site Marchand Vulnérable |
| S9 | 1 sem | Refactor Backend, Données & Tests |

---

## Sprint 10 — Nexus Messenger V1 : Temps réel WebSocket
**Durée : 1 sprint**
**Objectif : Assurer la réception des messages en temps réel sans rechargement de page.**

| Tâche | Description |
|-------|-------------|
| 10.1 | Fixer `esc is not defined` dans chat.html (bloquait l'affichage des messages reçus) |
| 10.2 | Ajouter l'event `join_conversation` côté backend avec accusé de réception |
| 10.3 | Ajouter la gestion de `message_error` côté frontend |
| 10.4 | Ajouter un fallback polling 3s pour les trous entre reconnexions WebSocket |

**Livrables :**
- Messages reçus en temps réel via WebSocket
- Fallback polling 3s si WebSocket indisponible
- Gestion des erreurs WebSocket (message_error, reconnexion auto)

**Total estimé : 9.5 semaines**

---

## Sprint 7 : (non réalisé — fusionné dans Sprint 6 et Sprint 8)
*Ce sprint n'a pas été exécuté individuellement. Les tâches prévues ont été redistribuées dans les sprints 6 (UI/UX) et 8 (Red Team).*

---

## Sprint 8 : Red Team & Site Marchand Vulnérable
**Durée : 2 semaines**
**Objectif : Ajouter un environnement Red Team avec un site e-commerce vulnérable (PHP + MySQL), SSH bruteforcable, un playground SQLi interactif et une interface divisée SOC/Red Team.**

| Tâche | US | Agent | Description |
|-------|----|-------|-------------|
| 8.1 | — | fullstack-developer | Créer le Dockerfile du lab `vuln-web-server` (PHP 8.2 Apache + MySQL + OpenSSH) |
| 8.2 | — | fullstack-developer | Créer la base de données e-commerce (init.sql : users, produits, commandes) |
| 8.3 | — | fullstack-developer | Développer les pages PHP e-commerce (index, login, products, product, admin, cart) avec injections SQL |
| 8.4 | — | fullstack-developer | Créer le script de démarrage (start.sh : MySQL → Apache → SSH), config SSH avec user admin |
| 8.5 | — | fullstack-developer | Créer le dictionnaire de brute force (30 mots) dans data/wordlist.txt |
| 8.6 | — | fullstack-developer | Implémenter `projet/backend/app/services/docker_service.py` (subprocess docker build/run/inspect/stop) |
| 8.7 | — | fullstack-developer | Créer `projet/backend/app/routers/redteam/labs.py` (start/stop/status, wordlist, bruteforce, proxy) |
| 8.8 | — | fullstack-developer | Enregistrer le router `redteam/labs` dans `projet/backend/app/main.py` |
| 8.9 | — | fullstack-developer | Mettre à jour `docker-compose.yml` : ajout service vuln-web-server, montage socket Docker |
| 8.10 | — | fullstack-developer | Mettre à jour le Dockerfile principal (montage socket Docker) |
| 8.11 | — | fullstack-developer | Restructurer `frontend/index.html` : onglets SOC / Red Team, nouvelle navigation |
| 8.12 | — | fullstack-developer | Développer la section Red Team dans `frontend/app.js` : lab control, SQLi playground, SSH brute force, attack log |
| 8.13 | — | fullstack-developer | Améliorer l'interface SOC : détails attaques, timeline, plus d'interactivité |
| 8.14 | — | fullstack-developer | Ajouter les styles Red Team dans `frontend/style.css` (progress bars, terminal, onglets) |
| 8.15 | — | tester | Tests unitaires : docker_service.py, router labs.py |
| 8.16 | — | tester | Tests d'intégration : workflow Red Team complet (start lab → SQLi → brute force → stop) |
| 8.17 | — | tester | Tests de non-régression sur tous les sprints précédents |

**Livrables :**
- Conteneur `vuln-web-server` fonctionnel (PHP + MySQL + SSH)
- Site e-commerce avec 4 points d'injection SQL
- Playground SQLi interactif dans l'interface
- Brute force SSH avec progression temps réel
- Interface splitée SOC / Red Team
- Dictionnaire de brute force fourni (30 mots)
- Tests fonctionnels et de non-régression

---

## Sprint 9 : Refactor Backend, Données & Tests
**Durée : 1 semaine**
**Objectif : Restructurer le backend en séparant clairement SOC et Red Team, enrichir les données CVE/MITRE, fiabiliser les endpoints, et exécuter les tests en boucle.**

| Tâche | US | Agent | Description |
|-------|----|-------|-------------|
| 9.1 | — | fullstack-developer | Restructurer `projet/backend/app/routers/` en sous-dossiers `soc/` et `redteam/` |
| 9.2 | — | fullstack-developer | Mettre à jour `main.py` pour importer depuis les nouveaux chemins |
| 9.3 | — | fullstack-developer | Ajouter le champ `service_count` dans `list_scans` + schema `ScanList` |
| 9.4 | — | fullstack-developer | Ajouter des endpoints de vérification : `GET /api/scans/health`, `GET /api/soc/status` |
| 9.5 | — | fullstack-developer | Enrichir `cve_data.py` : +20% de CVE sur plus de services (docker, tomcat, jenkins, elasticsearch, etc.) |
| 9.6 | — | fullstack-developer | Enrichir `mitre_data.py` : +20% de techniques MITRE associées aux nouvelles CVE |
| 9.7 | — | fullstack-developer | Ajouter un endpoint `GET /api/labs/status/detailed` avec infos complètes |
| 9.8 | — | fullstack-developer | Ajouter la validation des données entrantes (target validation, scan_type enum) |
| 9.9 | — | tester | Lancer les tests en boucle (5 itérations) avec vérification de non-régression |
| 9.10 | — | tester | Fixer tous les échecs jusqu'à obtenir 100% sur toutes les itérations |

**Livrables :**
- Backend restructuré SOC / Red Team
- Données CVE enrichies (nouveaux services)
- Endpoints fiabilisés avec validation
- Tests validés en boucle (5 runs)
- 100% de réussite sur tous les tests
