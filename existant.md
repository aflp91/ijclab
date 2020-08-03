L'existant comprend 2 applications distincts : les projets CodingPool et CodeGuards.


A l'origine le projet CodingPool avait pour ambition de proposer un système d'accès original aux tutoriels informatiques
créer au sein du laborateur qui c'est par la suite étendu aux tutoriels externes. 
Une première implémentation de ce service de référencement de tutoriels est disponible sur le WEB à l'URL : 
https://codingpool.in2p3.fr/


Une interface utilisateur ,codé en HTML, CSS, Vue.js, donne accès aux tutoriels internes et externes référencés par
les utilisateurs de l'application. Un back-end , codé en python avec le framework Flask, envoie l'ensemble des
ressources liées aux tutoriels et aux prescripteurs, auteurs et préparateurs de ces contenus pédagogiques en ligne.
Enfin une base de données, sqlite, permet de rendre les données persistante d'une connexion à l'autre.


Le site est une application web monopage (ou single page application, SPA), cet-à-dire une application web accèssible 
via une page web unique. Le but est d'éviter le chargement d'une nouvelle page à chaque action demandée, et fluidifier
ainsi l'expérience utilisateur. Cette interface est comprise dans un unique fichier html qui sera rendu par le serveur
lors de la première connexion. Cependant le système de tri par étiquette qui permet de filtrer les tutoriels est 
dépendant des données stockées sur le serveur. Ainsi lorque l'utilisateur filtre les tutoriels en sélectionnant
une étiquette des informations entre le client et le serveur seront échangées sous le format JSON. La page ne sera 
pas recharger, seul les tutriels et étiquettes servant à filtrer les tutoriels seront mis-à-jour.

plan
descriptions
critiques 
