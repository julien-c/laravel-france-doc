# Commandes d'Artisan 

## Au menu

- [Aide](#help)
- [Configuration de l'application](#application-configuration)
- [Sessions en base de données](#sessions)
- [Migrations](#migrations)
- [Bundles](#bundles)
- [Tâches](#tasks)
- [Tests unitaires](#unit-tests)
- [Routage](#routing)
- [Clé d'application](#keys)
- [Options en ligne de commandes](#cli-options)

<a name="help"></a>
## Aide

Description  | Commande
------------- | -------------
Affiche une liste de commandes disponibles. | `php artisan help:commands`

<a name="application-configuration"></a>
## Configuration de l'application <small>[(Plus d'infos)](/docs/v3/doc/install#basic-configuration)</small>

Description  | Commande
------------- | -------------
Génère une clé d'application sécurisée. Cette clé ne sera généré que si le champ est vide dans le fichier **config/application.php**. | `php artisan key:generate`

<a name="sessions"></a>
## Sessions en base de données <small>[(Plus d'infos)](/docs/v3/doc/session/config#database)</small>

Description  | Commande
------------- | -------------
Crée la table de sessions | `php artisan session:table`

<a name="migrations"></a>
## Migrations <small>[(Plus d'infos)](/docs/v3/doc/database/migrations)</small>

Description  | Commande
------------- | -------------
Crée la table de migration | `php artisan migrate:install`
Crée une migration | `php artisan migrate:make create_users_table`
Crée une migration pour un bundle  |  `php artisan migrate:make bundle::tablename`
Exécute les migrations en attentes  |  `php artisan migrate`
Exécute les migrations en attentes de l'application |  `php artisan migrate application`
Exécute les migrations en attentes d'un bundle  |  `php artisan migrate bundle`
Annule le dernière opération de migration | `php artisan migrate:rollback`
Annule toutes les opérations de migration  |  `php artisan migrate:reset`

<a name="bundles"></a>
## Bundles <small>[(Plus d'infos)](/docs/v3/doc/bundles)</small>

Description  | Commande
------------- | -------------
Installe un bundle  |  `php artisan bundle:install eloquent`
Mise à jour d'un bundle  |  `php artisan bundle:upgrade eloquent`
Mise à jour de tous les bundles | `php artisan bundle:upgrade`
Publie les assets d'un bundle | `php artisan bundle:publish bundle_name`
Publie les assets de tous les bundles | `php artisan bundle:publish`

<br>
> **Note:** Après l'avoir installé, vous devez [enregistrer le bundle](/docs/v3/doc/bundles/#registering-bundles)

<a name="tasks"></a>
## Tâches <small>[(Plus d'infos)](/docs/v3/doc/artisan/tasks)</small>

Description  | Commande
------------- | -------------
Appel une tâche  |  `php artisan notify`
Appel une tâche and passing arguments  |  `php artisan notify taylor`
Appel une une méthode spécifique d'une tâche  |  `php artisan notify:urgent`
Appel une tâche d'un bundle | `php artisan admin::generate`
Appel une une méthode spécifique d'une tâche de bundle  |  `php artisan admin::generate:list`

<a name="unit-tests"></a>
## Test unitaires <small>[(Plus d'infos)](/docs/v3/doc/testing)</small>

Description  | Commande
------------- | -------------
Exécute les tests de l'application  |  `php artisan test`
Exécute les tests unitaires d'un bundle  |  `php artisan test bundle-name`

<a name="routing"></a>
## Routage <small>[(Plus d'infos)](/docs/v3/doc/routing)</small>

Description  | Commande
------------- | -------------
Appel une route  |  `php artisan route:call get api/user/1`

<br>
> **Note:** vous pouvez remplacer get par post, put...

<a name="keys"></a>
## Clé d'application

Description  | Commande
------------- | -------------
Génère une clé d'application  |  `php artisan key:generate`

<br>
> **Note:** Vous pouvez spécifier en paramètre alternatif, une longueur pour la clé.

<a name="cli-options"></a>
## Options en ligne de commandes

Description  | Commande
------------- | -------------
Définition de l'environnement d'exécution  |  `php artisan foo --env=local`
Définition de la base de données par défaut  |  `php artisan foo --database=sqlitename`
