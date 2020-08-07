L'existant comprend 2 applications WEB : CodingPool et CodeGuard

Une interface utilisateur ,codé en HTML, CSS, Vue.js, donne accès aux tutoriels internes et externes référencés par
les utilisateurs de l'application. Un back-end , codé en python avec le framework Flask, envoie l'ensemble des
ressources liées aux tutoriels et aux prescripteurs, auteurs et préparateurs de ces contenus pédagogiques en ligne.
Enfin une base de données, sqlite, permet de rendre les données persistante d'une connexion à l'autre.


Le site est une application web monopage (ou single page application, SPA), cet-à-dire une application web accèssible 
via une page web unique. Le but est d'éviter le chargement d'une nouvelle page à chaque action demandée, et fluidifier
ainsi l'expérience utilisateur. Cette interface est comprise dans un unique fichier html qui sera rendu par le serveur
lors de la première connexion. Seul les parties dynamiques de la page, les labels et tutoriels, sont rechargées 
dynamiquement grâce à l'architecture AJAX. 

application monopage
tri de tutoriel
inscription connexion

plan
descriptions
critiques 

CodingPool est une application monopage CLIENT/SERVEUR. Elle délivre un ensemble de services asynchrone.
Ces services sont dit asynchrones car il requière une communication entre le CLIENT (ex. IE, FireFox, Safari)
et le SERVEUR (ex. APACHE, NGX). Un échange de données est fait entre les deux entités. Le CLIENT envoie une 
requête au SERVEUR qui répondra à la demande du client selon un plan prédéfini.
Contrairement au application WEB classique, le serveur ne renvoie pas de page HTML mais des données sous le 
format JavaScript Object Notation (JSON).L'application cliente se met à jour lorsqu'elle reçoit les données.
Le temps de communication entre le CLIENT et le SERVEUR est variable. L'ordre de grandeur est de quelques 
milisecondes à une dizaine de milisecondes. Ce qui est satisfaisant car peu ou pas visible à l'oeil nu.
Le client intéroge le serveur pour obtenir des informations sur la base de données :
Donnes moi les tutoriels disponibles
Donnes moi les étiquettes des tutoriels que tu m'a envoyer afin que je puisse continuer à filtrer.
Connecte moi au compte utilisateur ayant pour et email X et mot de passe Y.
...

Voici la liste exhaustive des fonctionnalités qui requière une communication entre le CLIENT et le SERVEUR :
-obtenir un jeu de tutoriels et leur étiquettes discriminantes de plus haut niveau
-filtrer les tutoriels
-créer un compte utilisateur
-se connecter à un compte utilisateur
-éditer la hiérarchie des labels
-ajouter un tutoriel dans la base de données
-afficher les publications d'un utilisateur donné
-authentifier un compte (admin)

Il existe également une méthode synchrone qui réutilise les données envoyer par le serveur : le changement de
langue de l'inerface.
Sauvegarder des données du serveur sur l'application cliente (le navigateur) est une stratégie efficace
pour limiter les aller-retour entre serveur et client et ainsi améliorer les performances de l'application. 
Idéalement cette façon de faire devrait-être utilisée le plus souvent possible. 
Elle a néanmoins des inconvénients concernant la persistance des données et la mise
à jour de celle-ci. En effet lorsque l'utilisateur veut écrire, supprimer ou mettre-à-jour des données, il est
préférable de communiquer avec le serveur rapidement, au risque de ne pas exécuter ces opérations. Par ailleurs
les données consultés en lecture par l'utilisateur peuvent-être périmées si elles ne sont pas mise-à-jour régulièment.
On constate en majorité que les interactions de l'utilisateur avec le système solicite grandement le serveur mais 
cette implémentation n'a pas d'effet délétaire sur les perfomances d'une application testé par un unique utilisateur 
et une base de données relativement vide.



Fonctionnalités :
+ interdir un label
+ obliger un label
+ filtrer les tutoriels
+ modifier la langue de navigation (en, fr) asynchrone ?
+ créer un compte utilisateur
* se connecter à son compte utilisateur
+ modifier la hierarchie des labels
+ ajouter un tutoriel
+ associer des utilisateurs aux rôles de comtribueur (prescriber), préparateur (preparator), demandeur (requestor)
+ associer un statut à l'élément ajouté 
+ associer un ou plusieurs labels à un tutoriel
+ gestion du statut non authentifié
+ gestion du statut d'admin
- envoie d'e-mail
- gestion du statut authentifié

interface utilisateur:
+ recherche graphique autour du thème de la piscine
+ fluidité de l'application
+ message d'information de l'API


GLOSSAIRE : 
-application monopage
-design patern store