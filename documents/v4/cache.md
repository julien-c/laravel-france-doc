# Cache

- [Configuration](#configuration)
- [Utilisation](#cache-usage)
- [Cache de base en données](#database-cache)

<a name="configuration"></a>
## Configuration

Laravel fournit une API unique pour différents gestionnaires de cache. La configuration du cache est située dans le fichier `app/config/cache.php`. Dans ce fichier, vous devez indiquer le driver à utiliser par défaut dans votre application. Laravel supporte les célèbres gestionnaires de cache [Memcached](http://memcached.org) et [Redis](http://redis.io).

De plus, le fichier de configuration du cache fournit diverses options. Consultez ces options, elles sont documentées directement dans le fichier de configuration. Par défaut, Laravel est configuré pour utiliser le gestionnaire de cache `file` lequel enregistre les objets sérialisés dans des fichiers. Pour les applications de grande envergure, il est recommandé d'utiliser un cache mémoire comme Memcached ou APC. 

<a name="cache-usage"></a>
## Utilisation

**Stocker une variable dans le cache**

	Cache::put('key', 'value', $minutes);

**Lire une variable dans le cache**

	$value = Cache::get('key');

**Lire une variable ou retourner une valeur par défaut**

	$value = Cache::get('key', 'default');

	$value = Cache::get('key', function() { return 'default'; });

**Stocker une variable dans le cache de manière permanente**

	Cache::forever('key', 'value');

Lors de la lecture d'une variable dans le cache, si vous souhaitez enregistrer une valeur par défaut dans le cas où la variable n'existe pas, utilisez la méthode `Cache::remember` :

	$value = Cache::remember('users', $minutes, function()
	{
		return DB::table('users')->get();
	});

Vous pouvez aussi combiner les méthodes `remember` et `forever` :

	$value = Cache::rememberForever('users', $minutes, function()
	{
		return DB::table('users')->get();
	});

Notez que les variables mises en cache étant sérialisées, n'importe quel type de variable peut être mis en cache.

**Supprimer une variable du cache**

	Cache::forget('key');

<a name="database-cache"></a>
## Cache de base de données

Pour utiliser le driver de cache `database`, vous devez créer une table destinée à stocker les variables de cache. Voici un exemple de création d'une telle table :

	Schema::create('cache', function($t)
	{
		$t->string('key')->unique();
		$t->text('value');
		$t->integer('expiration');
	});
