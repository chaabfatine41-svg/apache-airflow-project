# Apache Airflow

## 1. Introduction à Apache Airflow

Apache Airflow est une plateforme open source de gestion des workflows permettant de programmer, d’orchestrer et de surveiller des pipelines de données sous forme de graphes acycliques dirigés (DAGs).

Ses principales fonctions sont :
- **Orchestration :** définir l’ordre logique des tâches.
- **Monitoring :** suivre l’état des tâches et consulter les erreurs.
- **Scheduling :** planifier l’exécution des workflows.
- **Retry / Replay :** relancer les tâches en cas d’échec.

## 2. Historique

- **2014 :** création chez Airbnb.
- **2015 :** publication en open source sur GitHub.
- **2018 :** entrée dans l’Apache Incubator.
- **2019 :** devient un projet Apache de premier niveau (Top-Level Project).

## 3. Concepts fondamentaux

### 3.1. DAG (Directed Acyclic Graph)

Un DAG est un graphe orienté sans cycle. Il représente les tâches et leurs dépendances.

- **Nœuds :** représentent les tâches.
- **Arêtes :** définissent les dépendances entre les tâches.
- **Acyclique :** aucune tâche ne peut dépendre d’elle-même.

Les DAGs sont définis en Python. Une tâche ne démarre que lorsque ses dépendances sont satisfaites.

### 3.2. Tasks et Task Instances

- **Task :** définition d’une tâche à exécuter dans le DAG.
- **Task Instance :** exécution concrète d’une tâche lors d’un lancement du DAG.

Les états possibles comprennent :
- Queued : en attente.
- Running : en cours.
- Success : réussie.
- Failed : échouée.
- Skipped : ignorée.
- Retry : nouvelle tentative.

### 3.3. Scheduling

Le scheduling permet de programmer l’exécution des DAGs à des moments précis.

Exemple d’expression Cron :

`0 6 * * *`

Cette expression correspond à une exécution quotidienne à 6 h 00.

Autres exemples :
- `@daily` : chaque jour à minuit.
- `@hourly` : chaque heure.
- `@weekly` : chaque semaine.
- `@monthly` : chaque mois.

## 4. Architecture d’Apache Airflow

Les principaux composants sont :

### 4.1. Web Server
Fournit l’interface Web permettant de visualiser les DAGs, de consulter l’état des tâches et d’accéder aux logs.

### 4.2. Scheduler
Analyse les DAGs et détermine quelles tâches doivent être exécutées selon leur planification et leurs dépendances.

### 4.3. Executor
Détermine comment les tâches sont exécutées.

- **LocalExecutor :** exécution sur la même machine.
- **CeleryExecutor :** exécution distribuée sur plusieurs workers.

### 4.4. Metadata Database
Stocke les états des tâches et l’historique des exécutions.

### 4.5. Workers
Dans une architecture distribuée, les workers exécutent les tâches qui leur sont attribuées.

## 5. Fonctionnement global

1. Le développeur écrit un DAG en Python.
2. Le Scheduler identifie les tâches prêtes à être exécutées.
3. L’Executor organise leur exécution.
4. La Metadata Database conserve les informations relatives aux exécutions.
5. L’interface Web affiche les états des DAGs et des tâches.

Airflow orchestre les tâches et leurs dépendances. Il ne réalise pas nécessairement lui-même les traitements de données.

## 6. Types d’Operators

Un Operator définit l’action qu’une tâche doit effectuer.

### 6.1. PythonOperator
Permet d’exécuter une fonction Python.

Exemple :

```python
from airflow.operators.python import PythonOperator

def ma_fonction():
    print("Hello Airflow!")

task = PythonOperator(
    task_id="ma_tache",
    python_callable=ma_fonction
)
```

Cas d’utilisation : traitement de données, appels API et transformations ETL.

### 6.2. BashOperator
Permet d’exécuter une commande Bash ou un script Shell.

Exemple :

```python
from airflow.operators.bash import BashOperator

task = BashOperator(
    task_id="run_script",
    bash_command='echo "Pipeline lancé !"'
)
```

### 6.3. EmailOperator
Permet d’envoyer des e-mails et des notifications automatiques.

Paramètres principaux :
- `to` : destinataire.
- `subject` : objet du message.
- `html_content` : contenu du message.

### 6.4. SQL Operators
Permettent d’interagir avec des bases de données pour exécuter des requêtes SQL.

Exemples présentés :
- PostgreSQL.
- MySQL.
- SQLite.
- BigQuery.
- Microsoft SQL Server.

### 6.5. Sensors
Les Sensors attendent qu’une condition soit satisfaite avant de poursuivre l’exécution.

Exemples :
- `FileSensor` : attend l’apparition d’un fichier.
- `HttpSensor` : vérifie une réponse HTTP.
- `SqlSensor` : attend un résultat SQL.
- `ExternalTaskSensor` : attend la fin d’une tâche externe.
- `TimeSensor` : attend une heure précise.

## 7. Avantages et limites

### Avantages
- Flexibilité et extensibilité.
- Interface visuelle.
- Écosystème riche et nombreuses intégrations.
- Gestion des dépendances entre tâches.
- Solution open source.
- Planification et suivi des workflows.

### Limites
- Courbe d’apprentissage importante.
- Surcharge opérationnelle.
- Gestion complexe des DAGs volumineux.
- Adaptation limitée aux flux en temps réel.
- Intégrations parfois complexes.

## 8. Comparaison avec d’autres outils

### Apache Airflow
Solution mature, centrée sur les tâches et les DAGs, adaptée aux pipelines batch structurés et aux workflows complexes.

### Dagster
Approche centrée sur les données et les assets, avec des fonctionnalités de traçabilité et d’observabilité.

### Prefect
Approche Python flexible, orientée vers la simplicité d’utilisation et la création rapide de workflows.

## 9. Conclusion

Apache Airflow est une plateforme d’orchestration de workflows de données. Son modèle DAG permet de définir les tâches et leurs dépendances, tandis que le Scheduler, l’Executor et la Metadata Database contribuent à leur planification, leur exécution et leur suivi.

Airflow convient particulièrement aux pipelines de données structurés nécessitant une planification fiable, une surveillance et une gestion claire des dépendances.

**Remarque :** ce document reprend les principaux thèmes de la présentation académique. Les exemples de code sont des exemples présentés dans le rapport et ne constituent pas une preuve que le projet pratique a été exécuté avec succès.
