# Recipe Graph Assistant 

Ce projet implémente un chatbot intelligent capable de comprendre des questions en langage naturel concernant des recettes de cuisine, de les traduire en requêtes graphiques **Cypher**, puis d'interroger une base de données **Neo4j** pour retourner les ingrédients, les étapes de préparation ou des liens de recettes.

## 📋 Présentation du Projet
L'architecture repose sur le principe de la génération de requêtes assistée par un LLM (Text-to-Cypher) :
1. L'utilisateur pose une question en anglais sur une recette (ex: *"Could you provide the ingredients for Carrot Bread?"*).
2. Le modèle **Gemini-Pro** reçoit la question encapsulée dans un prompt d'ingénierie (*Few-Shot Prompting*) contenant le schéma du graphe et des exemples.
3. Le modèle génère la requête Cypher correspondante.
4. Le script nettoie et exécute la requête sur une instance de base de données **Neo4j**.
5. Les données brutes retournées sont formatées et affichées dans une interface utilisateur interactive **Gradio**.

## 📊 Schéma du Graphes (Neo4j)
Le graphe de connaissances culinaires est structuré de la manière suivante :
* **Labels des Noeuds :**
  * `Recette` (propriétés : `title`, `link`, `source`)
  * `Étape` (propriétés : `Id`, `description`)
  * `Ingrédient` (propriétés : `nom`, `mesure`)
* **Types de Relations :**
  * `(:Recette)-[:PREPARED_WITH_STEPS]->(:Étape)`
  * `(:Recette)-[:CONTIENT]->(:Ingrédient)`

## 🛠️ Technologies Utilisées
* **Python 3**
* **Google Generative AI (Gemini API)** : Modèle `gemini-pro` utilisé pour la traduction Text-to-Cypher.
* **Neo4j** (Driver Python) : Base de données orientée graphe pour stocker et interroger efficacement les relations culinaires.
* **Gradio** : Pour la création rapide de l'interface de chat.
* **RegEx (re)** : Pour le nettoyage et l'extraction des composants de requêtes.

## 🚀 Installation et Utilisation

### 1. Cloner le projet
```bash
git clone [https://github.com/NouhailaOULAARIF/recipe-graph-assistant.git](https://github.com/NouhailaOULAARIF/recipe-graph-assistant.git)
cd recipe-graph-assistant
