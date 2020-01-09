# TD Immobilier

> Projet de gestion de biens immobiliers

## Lancer le projet

Pour lancer le projet, utilisez la commande `npm run serve`

## Étapes 1: Récupération des informations sur les biens

La première étape consiste à récupérer les données depuis une API.

Aucun back-end n'est à votre disposition pour le moment, on va le simuler avec `json-server`.

À la racine du projet, lancez la commande `json-server --watch bdd.json`.

Nous utiliserons la librairie `axios` pour nos appels *HTTP*.
Pour ne pas perdre trop de temps avec la connexion internet, cette librairie a déjà été installée dans le projet via *npm* (`npm install --save axios`).

**Attendu**: Récupérez les données de l'API dans le composant racine de l'application (**App.vue**).

Vous pourrez vérifier que les données sont bien présentes grâce à l'outil *Vue Devtools*.

## Étape 2: Création d'un composant BienAVendre.vue

Maintenant que les données sont récupérées, nous allons pouvoir les afficher à l'utilisateur. Pour ce faire, nous allons créer un composant **BienAVendre.vue**.

Ce dernier doit être générique, et prendre en paramètre les informations d'un bien à vendre.

**Attendu**:
- Créez le nouveau composant dans lequel sont affichés les informations d'un bien à vendre;
- Affichez ce composant pour chaque bien récupéré depuis la base.

**Amélioration**:
- Découverte des *props* avancées: typez et donnez une valeur par défaut aux *props* reçues par **BienAVendre.vue**.

## Étape 3: Filtre sur les bien non vendus

Nos utilisateurs souhaitent avoir la possibilité de ne plus voir les biens vendus.

**Attendu**: Ajouter une gestion de filtre dans le composant **App.vue** afin de ne plus afficher tous les biens reçu depuis l'API, mais uniquement ceux qui restent à vendre.

## Étape 4: Achat d'un bien

Une fonctionnalité attendue de notre application est le fait de pouvoir marquer un bien comme "vendu". Pour le moment, n'importe qui pourra le faire en cliquant sur un simple bouton.

**Attendu**:
- Dans **BienAVendre.vue**, ajoutez un bouton pour marquer le bien comme "vendu";
- Au click sur ce bouton, faites un appel API pour mettre à jour le bien.

**Amélioration**:
- Découverte des *events*: Ne plus faire cette gestion dans **BienAVendre.vue** mais déléguer la responsabilité dans le composant **App.vue** (utiliser les [*custom events*](https://vuejs.org/v2/guide/components-custom-events.html)).

## Étape 5: Formulaire d'ajout de bien à vendre

La dernière fonctionnalité attendue est de pouvoir ajouter un bien à vendre.

Un formulaire présentant les informations suivantes doit être présent sur le site:

- Un titre pour l'offre;
- Le type de bien ("maison" ou "appartement" pour le moment);
- Le prix en €;
- Un contact (champ libre où l'utilisateur peut choisir de mettre un numéro de téléphone, une adresse, etc).

Tous ces champs sont obligatoires.

**Attendu**:
- Créez un composant **AjoutDeBien.vue** avec le formulaire et toutes ses règles de gestion (champs obligatoires);
- À la validation du formulaire, notifier **App.vue**;
- Dans **App.vue**, appeler l'API pour ajouter le bien.

## Bonus: Gestion des chargements et des erreurs

Vous pouvez chercher un moyen de rendre l'experience utilisateur plus fluide en indiquant des messages lors du chargement et en prévenant l'utilisateur que son action a échouée.

De plus, si un chargement a échoué, il serait intéressant de proposer un bouton pour tenter un nouveau chargement sans recharger la page entière.
