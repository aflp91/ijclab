# Plan de la partie existante

## Le projet CodingPool

  + Définition
      * catalogue de tutoriels
      * système de recherche par étiquettes
      * plateforme de recommandation et de publication de tutoriels
      * plateforme interactive (demande, préparation, publication)
  + Bref historique
      * qui
      * quand
      * combien de temps

## Application WEB

  + Les trois couches 
      * HTML
      * CSS
      * JavaScript
  + DOM
  + Programmation événementielle

## L'environnement technologique

  + Back end : Flask
      * micro framework Python
      * fullstack
      * architecture courante
          - MVC
          - API Rest
          - SPA
  + Front end : Vue.js
      * framework JavaScript
      * MVVM

## Architecture

  + Front end : MVVM 
  + Back end : SPA (single page+JSON)
  + CRUD

## Implémentation côté serveur

  + Modèle
      * étiquette
          - hiérarchie
          - association tutoriel/étiquette
      * tutoriel
      * utilisateur
      * alias
          - maintenabilité du système d'étiquettes
      * schéma
          - présentation
      * méthodes
          - fonctionnalités
  
  + Contrôleur
      * fonctionnement
          - associer les fonctionnalités à des requêtes sous forme d'URL (routes)
          - exemple : fichier `codingpool.py` qui contient toutes les routes de l'application
   
  + Problèmes adressés
      * minimum deux requêtes HTTP pour un résultat
          - solution : optimiser les échanges client-serveur
              + système de filtrage en JavaScript
              + une requête HTTP pour un résultat 
      * manquait d'organisation/structuration
          - solutions :
              + blueprint
              + organisation en sous-projets (LabelsTower, Codeguards)
      * routes administrateur non protégées
          - solution : implémenter un système d'authentification multirôle
      * manquait certaines fonctionnalités du cahier des charges
          - ajout de tutoriel
          - authentification des utilisateurs
      * quelques choix technologiques discutables
          - doublon d'accès à la BdD
              + solution : choisir entre SQLite et SQLAlchemy
          - refaire la roue (système de stockage, gestion des fonctions asynchrones)
              + solution : utiliser des technologies éprouvées
          - pas de fichier de configuration [à déplacer]

## Implémentation côté client
    
  + Modèle (M dans M.V.VM, Model View ViewModel)
      * les données récupérées et enregistrées dans le modèle client
      * les instances de Vue (`header`, `footer`, `hierarchy`, `result`) et leur modèle
          - `hierarchy`
          - `result`
      * communication avec le serveur
           - `HttpRequest`
           - `JSON response`

  + Problème
      * architecture
          - absence d'utilisation des composants
          - `is_login` géré dans plusieurs instances de Vue.js (`result`, `footer`)
              + mieux définir les rôles de chaque instance
              + communiquer l'état de `is_login` à `result` si besoin
          - script d'initialisation
               + utiliser les `life cycle hook` des instances Vue.js
      * gestion des fonctions asynchrones
           - solution : utiliser l'objet `Promise`

  + Vue (V dans M.V.VM, Model View ViewModel)
      * charte graphique sur le thème de la piscine
      * vue monolithique
      
        Reprendre une implémentation monolithique en composants logiques
