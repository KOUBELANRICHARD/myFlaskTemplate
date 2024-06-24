# MyFlaskTemplate

## Description

Ce projet est une application web créée avec le framework Python Flask et intégrant un template de base Bootstrap. L'objectif est de démontrer comment construire une application Flask, la conteneuriser avec Docker, puis déployer le conteneur sur un cluster Kubernetes via un pipeline CI/CD utilisant GitHub Actions.

## Structure du projet
```sh
MYFLASKTEMPLATE/
│
├── app/
│ ├── pycache/
│ ├── templates/
│ │ └── index.html
│ ├── app.py
│ └── requirements.txt
├── Dockerfile
├── k8s/
│ └── deployment.yaml
│ └── service.yaml
└── .github/
└── workflows/
└── main.yml
```

## Installation



1. Créer un environnement virtuel et installer les dépendances :
    ```sh
    python -m venv .venv
    source .venv/bin/activate  
    pip install -r requirements.txt
    ```

2. Lancer l'application :
    ```sh
    flask --app /app.py run
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

## Déploiement et exposer l' application sur un cluster Kubernetes de GCP

- Création du compte sur GCP
- Création du projet sur GCP
- Création du cluster sur GCP avec autopilot

    ### Si utilisation de cloud Shell de GCP alors 

    - Se connecter via cloud shell au cluster 
    - Créer le fichier deployement.yaml et service.yaml avec nano
    - Ensuite exécuter les fichiers avec kubectl avec les commandes suivantes : 
        ```sh
        kubectl apply -f deployment.yaml
        kubectl apply -f service.yaml
        ```

    ### Déploiement manuel via kubectl

    - Configuration de Kubectl pour utiliser le cluster GKE avec utilisation de google SDK
    - Déploiement manuel via le fichier deployment.yaml et service.yaml via l'outil kubectl
    - deployment.yaml telecharge l'image Docker depuis docker Hub dans le cluster KS8
        ```sh
        kubectl apply -f deployment.yaml
        kubectl apply -f service.yaml
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

