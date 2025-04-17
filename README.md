# myBank

Projet React & Symfony (Docker)

Ce projet contient une application web composée de deux parties :

- **Frontend (React)** : L'interface utilisateur construite avec React.
- **Backend (Symfony)** : L'API RESTful développée avec Symfony.

## Structure du projet

Le projet est structuré de la manière suivante :

```
/myBank
  ├── /frontend  # Code source du frontend React
  ├── /api       # Code source de l'API Symfony
```

## Prérequis

Avant de démarrer, assurez-vous d'avoir installé Docker et Docker Compose sur votre machine.

- **Docker** : [Installation Docker](https://docs.docker.com/get-docker/)
- **Docker Compose** : [Installation Docker Compose](https://docs.docker.com/compose/install/)

## Installation

1. **Cloner le dépôt**

   Clonez ce projet sur votre machine locale :

   ```bash
   git clone https://github.com/ABoudjemaa/myBank.git
   ```

2. **Accéder à l'application**

   ### Backend (Symfony)

   - Accédez au répertoire du projet :

     ```bash
     cd api
     ```

   - Configurez les variables d'environnement (`.env`) :

     ```env
     APP_ENV=dev
     APP_SECRET=
     DATABASE_URL="mysql://root:root@database:3306/mybank-api-database?serverVersion=9.1.0&charset=utf8mb4"
     CORS_ALLOW_ORIGIN='^https?://(localhost|127\.0\.0\.1)(:[0-9]+)?$'
     ```

   - Installez les dépendances :

     ```bash
     composer install
     ```

   - Construisez l'image Docker :

     ```bash
     docker-compose up
     ```

   - Effectuez les migrations :

     ```bash
     docker exec -it api-backend-1 bash
     cd project
     php bin/console d:m:m
     ```

   Votre application devrait être accessible sur `localhost:8082`.

   ### Frontend (React)

   - Accédez au répertoire du projet :

     ```bash
     cd front
     ```

   - Configurez les variables d'environnement (`.env`) :

     ```env
     NEXT_PUBLIC_API_BASE_URL="http://localhost:8082/api"
     ```

   - Construisez l'image Docker :

     ```bash
     docker build -t mybank-front .
     ```

   - Exécutez le conteneur :

     ```bash
     docker run -p 3001:3000 --name mybank-front-container mybank-front:latest
     ```

   Votre application devrait être accessible sur `localhost:3001`.
