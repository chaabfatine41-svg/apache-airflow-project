# Commandes Apache Airflow

## 1. Vérifier la version de Python

```bash
python3 --version
```

## 2. Vérifier la version de pip

```bash
pip3 --version
```

## 3. Créer le dossier du projet

```bash
mkdir -p ~/airflow-project
cd ~/airflow-project
```

## 4. Créer un environnement virtuel

```bash
python3 -m venv .venv
source .venv/bin/activate
```

## 5. Installer Apache Airflow

```bash
pip install "apache-airflow==3.1.8" --constraint "https://raw.githubusercontent.com/apache/airflow/constraints-3.1.8/constraints-3.12.txt"
```

## 6. Vérifier l'installation

```bash
airflow version
```

## 7. Démarrer Airflow

```bash
airflow standalone
```

## 8. Accéder à l'interface Web

http://localhost:8080

**Remarque :** ces commandes documentent les étapes d'installation et de démarrage. Le fonctionnement complet d'un DAG n'a pas encore été validé.
