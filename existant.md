## Plan de la partie existant

- Le projet codingpool
    + definition
        * catalogue de tutoriels
        * système de recherche par étiquettes
        * plateforme de recommandation et de publication de tutoriels
        * plateforme d'interaction (demande, préparation, publication)
    + bref historique
        * qui
        * quand
        * combien de temps

- Application WEB
    + Les trois couches 
        * HTML
        * CSS
        * Javascript
    + DOM
    + Programmation événementielle

- L'environnement technologique
    + back-end : Flask
        * micro framework Python
        * fullstack
        * architecture courante
            - MVC
            - API Rest
            - SPA
    + front-end : Vue
        * framework JavaScript
        * MVVM

- Architecture
    + front-end : MVVM 
    + back-end : SPA (single page+JSON)
    + CRUD

- Implémentation côté serveur
    + Modèle
        * étiquette
            - hierarchie
            - association tutoriel/étiquette
        * tutoriel
        * utilisateur
        * alias
            - maintenabilité du système d'étiquette
        * schéma
            - présentation
        * méthodes
            - fonctionnalités
    
    + Contrôleur
        * fonctionnement
            - associer les fonctionnalités à des requêtes sous forme d'URL (routes)
            - exemple : fichier `codingpool.py` qui contient toutes les routes de l'application
     
    + Problèmes adressés
        * minimum deux requêtes http pour un résultat
            - solution : optimiser les échanges client/serveur
                + système de filtrage en JavaScript
                + une requête HTTP pour un résultat 
        * manquait d'organisation/structuration
            - solutions
                + blueprint
                + organisation en sous projet (labelstower, codeguards)
        * routes administrateur non protégées
            - solution
                + implémenté un système d'authentification multi-rôle
        * manquait certaines fonctionnalités du cahier des charges
            - ajout de tutoriel
            - authentification des utilisateur
        * quelques choix technologiques discutables
            - doublon d'accès à la BdD
                + solution
                    - choisir entre sqlite3 et sqlalchemy
            - refaire la roue (système de stockage, gestion des fonctions asynchrones)
                + solution
                    - utiliser des technologies éprouvées
            - pas de fichier de configuration [à déplacer]

- Implémentation côté client
    
    + Modèle (M dans M.V.VM, Model View ViewModel)
        * les données récupérées et enregistrées dans le model client
        * les instances de Vue (`header`, `footer`, `hierarchy`, `result`) et leur modèle
            - `hierarchy`
            - `result`
        * communication avec le serveur
             - HttpRequest
             - JSON response
    + Problème
        * architecture
            - absence d'utilisation des composants
            - `is_login` géré dans plusieurs instance de Vue.js (`result`, `footer`)
                + mieux définir les rôles de chaque instance
                + communiquer l'état de `is_login` à `result` si besoin
            - script d'initialisation
                 + utiliser les `life cycle hook` des instance Vue.js
        * gestion des fonctions asynchrones
             - solution
                 - utilisé l'objet Promise
    + Vue (V dans M.V.VM, Model View ViewModel)
    
        * charte graphique sur le thème de la piscne
        * vue monolitique
          Reprendre une implémentation monolitique en composants logiques