# Intéractions avec les bases de données

- [Configuration](#configuration)
- [Exécuter des requêtes](#running-queries)
- [Accéder aux connexions](#accessing-connections)

<a name="configuration"></a>
## Configuration

La connexion à une base de données et l'exécution d'une requête sont extrêmement simples à mettre en oeuvre avec Laravel. Configurer l'accès à la base de données s'effectue dans le fichier `app/config/database.php`. Les connexions et celle à utiliser par défaut peuvent être définies dans ce fichier. Le fichier contient des exemples pour tous les gestionnaires de base de données supportés.

Au début de l'année 2013, Laravel supporte MySQL, Postgres, SQLite et SQL Server.

<a name="running-queries"></a>
## Exécuter des requêtes

Une fois la connexion configurée, vous pouvez exécuter des requêtes à l'aide de la classe `DB`.

**Exécuter une commande Select**

	$results = DB::select('select * from users where id = ?', array(1));

La méthode `select` retourne un tableau de lignes.

**Exécuter une commande Insert**

	DB::insert('insert into users (id, name) values (?, ?)', array(1, 'Dayle'));

**Exécuter une commande Update**

	DB::update('update users set votes = 100 where name = ?', array('John'));

**Exécuter une commande Delete**

	DB::delete('delete from users');

> **Remarque:** Les commandes `update` et `delete` retournet le nombre de lignes affectées par l'opération.

**Exécuter une requête quelconque**

	DB::statement('drop table users');

<a name="accessing-connections"></a>
## Accéder aux Connexions

Lorsque plusieurs connexions sont ouvertes, vous pouvez accéder à la connexion de votre choix à l'aide de la méthode `DB::connection` :

	$users = DB::connection('foo')->select(...);
