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
Contrairement au application WEB classique, le serveur ne renvoie pas uniquement des pages HTML mais aussi des 
données sous le format JavaScript Object Notation (JSON). L'application cliente se met à jour lorsqu'elle reçoit 
les données.
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


travail à implémenter :
-l'existant n'utilse pas assez les composants vuejs. Les composants pourraient-être décomposés en sous composants
 indépendants. Regrouper le code en sous composants indépendants augmente la lisibilité, la maintenabilité et 
 la réutilisabilité du code. Les composants existants sont des sortes de couteaux suisses et leur rôle devient
 incertain. Par exemple, le panneau des résultats affiche les résultats du filtrages des tutoriels, 
 les publications de chaque utilisateur, les formiulaires de connexion et inscription.
 Chacun de ces exemples nécessiterait un composant à part entière. L'implémentation existante n'est pas adapté
 à la conception de l'application monopage qui doit afficher diverse éléments dans une même partie de l'interface
 graphique (panneau des résultat). L'implémentation a accumulé un grand nombre de rendu conditionnelle sur un même
 composant. Par la suite d'autre fonctionnalité devaient apparaitre dans cette même partie de l'interface mais 
 le développeur à choisi d'abandonner le rendu conditionnel et à créer une nouvelle page html. Le principe 
 d'application monopage n'était plus respecté.

 -L'API permet au client de créer, mettre à jour ou récupérer des données sur le serveur. 
  Ces données concernent différents objet conceptuel de l'application codingpool : 
  les étiquettes, les tutoriels, les utilisateur.
  Les données sont renvoyés dans le format JavaScript Notation Object (JSON). Ce format est 
  directement interprétable par le viewModel qui sert à afficher des variables dans la page HTML.
  L'API évite le rafraichissement total de la page. Les quantités de données échangé entre le serveur et le 
  client diminue et ainsi les performances de vitesse de réaction de l'application augmentes.
  Cependant ces échanges de données ont tout de même un coup sur la performance. Il est donc préférable de 
  diminuer ces échanges au strict minimum. Malheuresement l'existant échange des données avec le serveur 
  constament. L'implémentation du design partern store serait bien adapté au filtrage des tutoriels qui 
  représente la plupart des échanges avec le serveur. Ce design partern consiste à récupérer toutes les
  données du serveur afin de les traités sur le client. Nous pourrions donc récupérer tout les tutoriels et
  étiquettes pour implémenter un filtrage local qui ne bloquerait pas le serveur.
  Ce design patern a des inconvénients. Le téléchargement de l'ensemble des données du serveur peut-être long
  et les données téléchargées sur le client peuvent ne plus être à jour. 

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