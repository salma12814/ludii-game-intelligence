::: {align="center"}
# 🏺 Ludii Game Intelligence

### Intelligence artificielle pour l'archéologie ludique

**Identifier · Contextualiser · Reconstruire**

Une plateforme d'IA qui combine vision par ordinateur, graphe de
connaissances et génération augmentée par récupération pour analyser des
jeux de table historiques à partir d'images, de descriptions ou de
caractéristiques de plateau.

[![Python](https://img.shields.io/badge/Python-3.11+-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/API-FastAPI-009688?logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![YOLOv8](https://img.shields.io/badge/Computer%20Vision-YOLOv8-111F68)](https://github.com/ultralytics/ultralytics)
[![Neo4j](https://img.shields.io/badge/Knowledge%20Graph-Neo4j-008CC1?logo=neo4j&logoColor=white)](https://neo4j.com/)
[![Streamlit](https://img.shields.io/badge/UI-Streamlit-FF4B4B?logo=streamlit&logoColor=white)](https://streamlit.io/)
[![n8n](https://img.shields.io/badge/Workflow-n8n-EA4B71)](https://n8n.io/)
:::

------------------------------------------------------------------------

## 📌 Présentation

Les jeux de table historiques sont des témoins précieux des
civilisations, mais leur étude est compliquée par les variantes
régionales, les informations historiques incomplètes et les plateaux ou
pièces endommagés. **Ludii Game Intelligence** propose une approche
intégrée pour assister leur analyse.

À partir d'une image ou d'une description, la plateforme peut détecter
les pièces, construire une représentation exploitable du plateau,
rechercher des jeux candidats dans un graphe de connaissances et fournir
un contexte historique. Elle inclut également des fonctionnalités de
recherche en langage naturel, de comparaison de jeux, de détection de
pièces potentiellement manquantes et de reconstruction 3D.

Le projet s'appuie sur la base de jeux **Ludii** et associe plusieurs
composants d'IA dans une application accessible par une interface
Streamlit, une API REST FastAPI et des workflows n8n.

## ✨ Fonctionnalités principales

  -----------------------------------------------------------------------
  Fonctionnalité                      Description
  ----------------------------------- -----------------------------------
  📷 **Identification par image**     Détection du plateau et des pièces
                                      avec YOLOv8, puis recherche de jeux
                                      candidats.

  📐 **Identification par             Recherche à partir de dimensions et
  dimensions**                        de caractéristiques partielles du
                                      plateau.

  🧠 **Raisonnement historique**      Exploitation d'un graphe Neo4j
                                      reliant jeux, règles, régions,
                                      périodes et catégories.

  🔗 **Jeux apparentés**              Exploration des relations du graphe
                                      pour trouver des jeux partageant un
                                      contexte ou des caractéristiques.

  💬 **Questions-réponses (RAG)**     Réponses en langage naturel
                                      contextualisées par des
                                      informations récupérées, avec
                                      Gemini.

  🧩 **Plateaux incomplets**          Comparaison entre les
                                      caractéristiques observées et
                                      attendues pour aider à repérer les
                                      éléments manquants.

  🏗️ **Reconstruction 3D**            Génération de modèles de plateau
                                      interactifs au format GLB avec
                                      Trimesh.

  📊 **Tableau de bord analytique**   Exploration des indicateurs et de
                                      la distribution du corpus de jeux.

  🔄 **Orchestration**                Possibilité d'enchaîner les
                                      traitements à l'aide de workflows
                                      n8n.
  -----------------------------------------------------------------------

## 🧩 Architecture

``` text
                         ┌───────────────────────────────┐
                         │        Utilisateurs            │
                         └───────────────┬───────────────┘
                                         │
                    ┌────────────────────┼───────────────────┐
                    │                    │                   │
              ┌─────▼─────┐        ┌─────▼─────┐       ┌─────▼─────┐
              │ Streamlit │        │  Swagger  │       │    n8n    │
              │ Interface │        │ API docs  │       │ Workflows │
              └─────┬─────┘        └─────┬─────┘       └─────┬─────┘
                    └────────────────────┼───────────────────┘
                                         │
                                  ┌──────▼──────┐
                                  │   FastAPI   │
                                  │  REST API   │
                                  └──────┬──────┘
                                         │
               ┌─────────────────────────┼─────────────────────────┐
               │                         │                         │
        ┌──────▼──────┐          ┌───────▼──────┐          ┌───────▼──────┐
        │   YOLOv8    │          │    Neo4j     │          │  Hybrid RAG  │
        │ Vision      │          │ Knowledge    │          │ Embeddings + │
        │ Detection   │          │ Graph        │          │ Gemini       │
        └──────┬──────┘          └───────┬──────┘          └──────────────┘
               │                         │
               └──────────────┬──────────┘
                              │
                    ┌─────────▼─────────┐
                    │ Identification,   │
                    │ contextualisation │
                    │ et reconstruction│
                    └───────────────────┘
```

### Chaîne d'analyse

1.  **Entrée** --- l'utilisateur fournit une image, des dimensions ou
    une description.
2.  **Perception** --- le module de vision détecte le plateau et/ou les
    pièces lorsque l'entrée est une image.
3.  **Structuration** --- les détections et caractéristiques sont
    transformées en données exploitables.
4.  **Identification** --- le système compare les caractéristiques
    observées aux signatures et informations du graphe.
5.  **Enrichissement** --- Neo4j sert à explorer les relations
    historiques et les jeux apparentés.
6.  **Restitution** --- l'application présente les résultats, peut
    générer une reconstruction 3D et permet de poser des questions en
    langage naturel via le RAG.

## 📚 Base de connaissances

Les chiffres du rapport et du dépôt décrivent le graphe construit à
partir des données Ludii :

  Indicateur                           Valeur rapportée
  -------------------------------- --------------------
  Jeux documentés                             **1 621**
  Rulesets / ensembles de règles              **3 337**
  Signatures visuelles                          **486**
  Régions historiques                            **28**
  Périodes chronologiques                        **13**
  Catégories de jeux                             **52**
  Relations dans le graphe           **environ 16 739**

Le corpus couvre des jeux de différentes régions et périodes, des jeux
anciens comme le Senet aux variantes d'échecs.

> **À noter :** le rapport signale des métadonnées géographiques
> absentes pour environ 35 % des jeux et des métadonnées chronologiques
> absentes pour environ 55 %. Il mentionne aussi 16 signatures YOLO
> orphelines. Ces limites peuvent réduire la couverture de certaines
> recherches contextuelles.

## 🔬 Module de vision : données et évaluation

Le corpus de détection a été constitué à partir d'images **synthétiques
générées avec le moteur Ludii**, puis annotées avec Roboflow et
exportées au format YOLO. Le modèle retenu est **YOLOv8 Nano**, choisi
pour son compromis entre rapidité d'inférence et coût de calcul.

Résultats rapportés dans le PFA sur l'ensemble de test **synthétique** :

  Métrique           Résultat
  -------------- ------------
  mAP@0.5          **0,9950**
  mAP@0.5:0.95     **0,9950**
  Précision        **0,9997**
  Rappel           **1,0000**

Ces résultats sont ceux du test synthétique décrit dans le rapport ; ils
ne doivent pas être interprétés comme une garantie de performance
équivalente sur des photographies archéologiques réelles. Une évaluation
sur des images réelles variées reste importante pour mesurer la
généralisation du modèle.

## 🛠️ Stack technique

  -----------------------------------------------------------------------
  Composant                           Technologie
  ----------------------------------- -----------------------------------
  Langage principal                   Python 3.11

  Détection d'objets                  Ultralytics YOLOv8 Nano

  Graphe de connaissances             Neo4j 5.x, Cypher

  API REST                            FastAPI, Uvicorn, Pydantic

  Interface web                       Streamlit

  RAG / modèle de langage             Sentence Transformers
                                      (`all-MiniLM-L6-v2`) et Gemini

  Reconstruction 3D                   Trimesh, format GLB

  Visualisation                       Plotly

  Orchestration                       n8n, Docker

  Source de connaissances ludique     Base et moteur Ludii
  -----------------------------------------------------------------------

## 📁 Organisation du dépôt

``` text
ludii-game-intelligence/
├── docs/                 # Documentation du projet
├── models/               # Modèles et artefacts associés
├── phase1_ludii_rag/      # RAG hybride : embeddings, Gemini et recours au graphe
├── phase2_vision/         # Détection du plateau/des pièces et reconstruction 3D
├── phase3_api/            # API FastAPI et routes applicatives
├── phase4_neo4j/          # Import, enrichissement et requêtes du graphe
├── phase5_n8n/            # Workflows d’orchestration
├── phase6_advanced/       # Fonctionnalités avancées
├── tests/                 # Tests
├── app.py                 # Interface Streamlit
├── requirements.txt       # Dépendances Python
├── Dockerfile
├── docker-compose.yml
└── README.md
```

## 🚀 Installation et démarrage

### Prérequis

-   Python **3.11+**
-   Neo4j **5.x** accessible localement ou sur un serveur
-   Une clé API Gemini pour les fonctionnalités RAG utilisant le modèle
-   Docker, si vous souhaitez exécuter n8n ou les services conteneurisés

### 1. Cloner le dépôt

``` bash
git clone https://github.com/salma12814/ludii-game-intelligence.git
cd ludii-game-intelligence
```

### 2. Créer l'environnement Python

**Windows (PowerShell)**

``` powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

**Linux / macOS**

``` bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### 3. Configurer les variables d'environnement

Créez un fichier `.env` à partir du modèle fourni :

``` bash
cp .env.example .env
```

Sous Windows, vous pouvez aussi copier manuellement `.env.example` vers
`.env`.

Renseignez les valeurs correspondant à votre environnement :

``` dotenv
NEO4J_URI=bolt://localhost:7687
NEO4J_USER=neo4j
NEO4J_PASSWORD=your_neo4j_password
GEMINI_API_KEY=your_gemini_api_key
```

Ne publiez jamais vos clés API ni vos mots de passe dans GitHub.

### 4. Construire / enrichir le graphe Neo4j

Démarrez Neo4j et exécutez les scripts d'importation dans l'ordre
indiqué par le projet :

``` bash
python phase4_neo4j/import_mysql_to_neo4j.py
python phase4_neo4j/import_lud_signatures.py
python phase4_neo4j/import_regions_periods.py
python phase4_neo4j/import_rules_features.py
```

Cette étape dépend des sources de données et des fichiers nécessaires
présents dans votre environnement. Vérifiez les chemins et la
configuration avant de lancer l'import.

### 5. Démarrer l'API FastAPI

À la racine du projet :

``` bash
uvicorn phase3_api.main:app --reload --host 127.0.0.1 --port 8000
```

Documentation interactive : <http://localhost:8000/docs>

### 6. Démarrer l'interface Streamlit

Dans un autre terminal, avec le même environnement Python activé :

``` bash
streamlit run app.py
```

Interface : <http://localhost:8501>

### 7. (Optionnel) Démarrer n8n

Si Docker est installé :

``` bash
docker run -d --name n8n -p 5678:5678 n8nio/n8n
```

Interface n8n : <http://localhost:5678>

Importez ensuite le workflow fourni dans le dépôt, s'il est présent dans
la version récupérée.

## 🧪 Exemples de requêtes API

Les routes ci-dessous correspondent aux exemples documentés dans le
dépôt. L'API doit être démarrée au préalable.

### Identification à partir de dimensions

``` bash
curl -X POST "http://localhost:8000/api/v1/identify_game_from_yolo" \
  -H "Content-Type: application/json" \
  -d '{"board_cols": 8, "board_rows": 8, "total_pieces": 32, "pieces": []}'
```

### Question en langage naturel

``` bash
curl "http://localhost:8000/api/v1/rag/ask?question=Explique-moi%20les%20règles%20du%20Senet"
```

Les champs requis et les paramètres acceptés peuvent évoluer ; consultez
la documentation Swagger à `/docs` pour le schéma exact de la version
installée.

## 🖥️ Services locaux

  Service           Adresse par défaut
  ----------------- ---------------------------------------------------
  API FastAPI       [localhost:8000](http://localhost:8000)
  Swagger UI        [localhost:8000/docs](http://localhost:8000/docs)
  Streamlit         [localhost:8501](http://localhost:8501)
  n8n (optionnel)   [localhost:5678](http://localhost:5678)
  Neo4j Browser     [localhost:7474](http://localhost:7474)

## 🎓 Contexte académique

Projet de fin d'année réalisé à l'**École Nationale Supérieure
d'Informatique et d'Analyse des Systèmes (ENSIAS)**, filière **Data &
Software Sciences**, année universitaire **2025--2026**.

**Intitulé :** *Ludii Game Intelligence: Système Intelligent de
Reconnaissance, Raisonnement et Reconstruction des Jeux de Table
Historiques*

-   **Réalisé par :** Soukaina Sabbar et Salma Issam
-   **Encadrant :** Pr. Khalid Nafil
-   **Jury :** Pr. Mohamed Radouane
-   **Soutenance :** 19 juin 2026

## 🔭 Pistes d'amélioration

En cohérence avec les limites identifiées dans le rapport, les pistes
suivantes sont pertinentes :

-   Évaluer le détecteur sur des photographies réelles, avec des
    conditions de lumière, de perspective et d'usure variées.
-   Améliorer la couverture des métadonnées géographiques et
    chronologiques.
-   Résoudre les associations de signatures visuelles qui restent
    orphelines.
-   Mesurer séparément la qualité de l'identification, la détection des
    pièces manquantes et la pertinence des réponses RAG.
-   Documenter les dépendances externes, les variables de configuration
    et les procédures de déploiement de façon reproductible.

## 📄 Rapport du projet

Le rapport de PFA présente le contexte, l'état de l'art, l'analyse et la
conception, la constitution du jeu de données de vision, le graphe Neo4j
et l'intégration de la plateforme. Si vous souhaitez le consulter
directement depuis GitHub, ajoutez le PDF au dépôt (par exemple dans
`docs/`) et créez ici un lien relatif vers son nom exact.

## 👥 Équipe

-   **Salma Issam**
-   **Soukaina Sabbar**

## 📜 Licence

Le README initial du dépôt indique une licence MIT. Vérifiez que le
fichier `LICENSE` correspondant est bien présent et cohérent avec les
dépendances et ressources externes utilisées avant toute redistribution.

------------------------------------------------------------------------

::: {align="center"}
**Ludii Game Intelligence**\
*L'intelligence artificielle au service du patrimoine ludique.*
:::
