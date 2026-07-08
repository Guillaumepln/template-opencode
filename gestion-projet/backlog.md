# Backlog Projet SOC Analyser

## User Stories

### US1 - Scan Réseau
En tant qu'analyste SOC, je veux pouvoir lancer un scan Nmap depuis une IP ou une plage d'IP afin de découvrir les hôtes actifs.

**Critères d'acceptation :**
- Saisie d'une IP unique ou d'un CIDR (ex: 192.168.1.0/24)
- Lancement du scan en arrière-plan
- Affichage des hôtes découverts avec leur statut

### US2 - Découverte de services
En tant qu'analyste SOC, je veux connaître les services et versions exposés sur chaque hôte afin d'évaluer la surface d'attaque.

**Critères d'acceptation :**
- Détection du nom du service (HTTP, SSH, etc.)
- Version du service détectée
- Port et protocole associé

### US3 - Corrélation CVE
En tant qu'analyste SOC, je veux que les services détectés soient corrélés avec des CVE afin d'identifier les vulnérabilités connues.

**Critères d'acceptation :**
- Mapping service/version → CVE
- Score CVSS associé
- Niveau de criticité (Critique, Élevé, Moyen, Faible)

### US4 - Corrélation MITRE ATT&CK
En tant qu'analyste SOC, je veux voir les techniques MITRE ATT&CK associées aux services/vulnérabilités détectées afin de comprendre le contexte d'attaque.

**Critères d'acceptation :**
- Techniques MITRE ATT&CK liées aux CVE
- Matrice tactique/technique affichée
- ID de technique (ex: T1190)

### US5 - Export CSV
En tant qu'analyste SOC, je veux exporter les résultats d'analyse en CSV afin de les intégrer dans d'autres outils.

**Critères d'acceptation :**
- Export de tous les résultats (hôtes, services, CVE)
- Format CSV standard avec en-têtes
- Téléchargement depuis l'interface

### US6 - Export JSON
En tant qu'analyste SOC, je veux exporter les résultats en JSON afin de les traiter par programmation.

**Critères d'acceptation :**
- Export structuré en JSON
- Téléchargement depuis l'interface
- Compatible avec des pipelines d'analyse

### US7 - Brute Force SSH
En tant qu'analyste SOC, je veux lancer un brute force SSH via Hydra sur un hôte cible afin de tester la robustesse des mots de passe.

**Critères d'acceptation :**
- Paramétrage de la cible (IP, port, userlist, passlist)
- Lancement du brute force en arrière-plan
- Affichage des identifiants trouvés

### US8 - Automatisation scan → brute force
En tant qu'analyste SOC, je veux automatiser le workflow complet : scan réseau → découverte SSH → brute force, à partir d'un fichier d'export Nmap.

**Critères d'acceptation :**
- Import d'un fichier XML Nmap existant
- Extraction automatique des services SSH
- Lancement du brute force sur les cibles SSH découvertes

### US9 - Dashboard UI/UX
En tant qu'analyste SOC, je veux un tableau de bord moderne avec métriques détaillées et code couleur par niveau de dangerosité.

**Critères d'acceptation :**
- Métriques : nb hôtes, services, CVE critiques, etc.
- Code couleur (rouge critique, orange élevé, etc.)
- Navigation fluide, responsive

### US10 - Historique des analyses
En tant qu'analyste SOC, je veux consulter l'historique de mes analyses afin de suivre l'évolution du parc.

**Critères d'acceptation :**
- Liste chronologique des scans
- Détail d'une analyse passée
- Suppression d'une analyse

### US11 - Conteneurisation
En tant qu'administrateur, je veux déployer l'application dans un seul conteneur Docker afin de simplifier l'installation.

**Critères d'acceptation :**
- Dockerfile multi-stage (backend + frontend)
- Un seul point d'entrée
- Documentation de déploiement
