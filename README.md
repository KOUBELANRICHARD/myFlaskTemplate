# MyFlaskTemplate

## Description

Ce projet est une application web créée avec le framework Python Flask et intégrant un template de base Bootstrap. L'objectif est de démontrer comment construire une application Flask, la conteneuriser avec Docker, puis déployer le conteneur sur un cluster Kubernetes via un pipeline CI/CD utilisant GitHub Actions.

## Structure du projet

MYFLASKTEMPLATE/
│
├── app/
│ ├── pycache/
│ ├── templates/
│ │ └── index.html
│ ├── app.py
│ └── requirements.txt
├── Dockerfile
└── .github/
└── workflows/
└── main.yml


## Installation

1. Cloner le repository :
    ```sh
    git clone <URL_de_votre_repository_github>
    cd MYFLASKTEMPLATE
    ```

2. Créer un environnement virtuel et installer les dépendances :
    ```sh
    python -m venv venv
    source venv/bin/activate  # Sur Windows, utilisez `venv\Scripts\activate`
    pip install -r requirements.txt
    ```

3. Lancer l'application :
    ```sh
    python app/app.py
    ```

## Conteneurisation avec Docker

1. Construire l'image Docker :
    ```sh
    docker build -t myflasktemplate .
    ```

2. Exécuter le conteneur :
    ```sh
    docker run -p 5000:5000 myflasktemplate
    ```

## Déploiement CI/CD avec GitHub Actions

Le pipeline CI/CD utilise GitHub Actions pour :

- Construire l'image Docker
- Pousser l'image sur Docker Hub
- Déployer l'image sur un cluster Kubernetes

## Fichier `Dockerfile`

```Dockerfile
FROM python:3.12
WORKDIR /app
COPY ./app /app
RUN pip install -r requirements.txt
EXPOSE 5000
CMD ["python", "app.py"]

