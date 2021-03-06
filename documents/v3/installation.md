# Installation et configuration

## Au menu

- [Pré-requis](#requirements)
- [Installation](#installation)
- [Configuration du serveur](#server-configuration)
- [Configuration basique](#basic-configuration)
- [Environnements](#Environnements)
- [Des URLs propres](#cleaner-urls)

<a name="requirements"></a>
## Pré-requis

- Apache, nginx, ou tout autre serveur web compatible PHP 5.3
- Laravel exploite les fonctionnalités introduitent par PHP 5.3. PHP 5.3 est donc un pré-requis.
- Laravel utilise la [library FileInfo](http://php.net/manual/fr/book.fileinfo.php) pour detecter le type mime des fichiers. Ceci est inclu par défaut dans PHP 5.3, cependant les utilisateurs de windows doivent ajouter une ligne dans leur php.ini pour autoriser le module. Pour plus d'informations, regardez veuillez vous réferer à la [page d'installation sur PHP.net](http://php.net/manual/fr/fileinfo.installation.php).
- Laravel utilise la [library Mcrypt](http://php.net/manual/fr/book.mcrypt.php) pour le chiffrage et cryptage de données. Mcrypt est souvent pré-installé. Si vous ne voyez pas Mcrypt lors d'un `phpinfo()`, alors regardez la [page d'installation sur PHP.net](http://php.net/manual/fr/book.mcrypt.php).

<a name="installation"></a>
## Installation

1. [Télécharger Laravel](/telecharger)
2. Extraire le contenu de l'archive et le mettre sur votre serveur web, ou poste de developpement.
3. Renseignez la valeur de l'option **key** dans le fichier **application/config/application.php** pour y placer une chaine de de 32 caractères aléatoires. Vous pouvez faire ceci depuis la ligne de commande grâce à **Artisan** : `php artisan key:generate`
4. Verifiez les droits d'écriture sur le dossier **storage** et ses sous dossiers.
5. Naviguez vers la page web.

Si tout est ok, vous verrez un magnifique splash screen Laravel. Soyez prêt, le voyage va commencer !

### Goodies

Les composants suivant ne sont pas nécéssaires, mais peuvent être utile pour exploiter pleinement Laravel : 

- Les drivers PDO de SQLite, MySQL, PostgreSQL, ou SQL Server.
- Memcached ou APC.

### Un problème ?

Si vous avez un problème, veuillez vérifier les points suivants :

- Assurez vous que le dossier **public** est défini en tant que DocumentRoot de votre serveur web. (voir: Configuration du serveur ci dessous)
- Si vous utilisez le mod_rewrite d'apache, inserer une chaine de caractères vide dans l'option **index** du fichier **application/config/application.php**.
- Vérifiez les droits d'écriture sur le dossier **storage** et ses sous dossiers.

<a name="server-configuration"></a>
## Configuration du serveur

Comme la plupart des framewoks de développement web, Laravel est conçu pour proteger le code source de votre application, de vos bundles et des document stockés dans le dossier **stoage**. Pour cela, Laravel place uniquement les fichiers nécéssaires dans le dossier **public**, qui doit être le DocumentRoot du serveur web. Cela évite que sur un serveur mal configuré, votre code source, incluant les informations de connexion à la base de données, ne soit accessible directement par le serveur web.

Pout cet exemple, imaginons que vous ayez installer Laravel dans le dossier **/Users/Jean/Sites/MonSite**.

Voici un exemple de VirtualHost Apache pour MonSite ressemblerai à cela :

    <VirtualHost *:80>
        DocumentRoot /Users/Jean/Sites/MonSite/public
        ServerName monsite.dev
    </VirtualHost>

Remarquez que nous avons installer le site dans le dossier **/Users/Jean/Sites/MonSite**, mais que notre DocumentRoot pointe sur **/Users/Jean/Sites/MonSite/public**.

Pointer le DocumentRoot vers le dossier **public** est une bonne pratique, à utiliser lorsque c'est possible. Mais avec certains hebergeurs, cela pourrait ne pas être possible. Vous trouverez des méthodes de contournements [sur les forums de Laravel[en].](http://forums.laravel.com/viewtopic.php?id=1258)

<a name="basic-configuration"></a>
## Configuration basique

Tous les fichiers de configurations fournies se trouvent dans le dossier config/ de votre application. Nous vous recommendons d'y jeter un oeil, afin de voir et de comprendre basiquement les options qui s'offrent à vous. Vous pouvez porter une attention spécial au fichier **application/config/application.php**, car il contient les options de configuration basique de votre application.

Il est **extrêmement** important de changer l'option **key** avant de commencer à travailler, ou même de visiter votre site. Cette clé est utilisée par le framework pour le cryptage, le chiffrage, ect... L'option se trouve dans le fichier **application/config/application.php** et doit être défini en tant que chaine de 32 caractères. Pour généré facilement une clé qui respecte le standard, vous pouvez utiliser l'outil en ligne de commande Artistan. Plus d'informations sur la page des [commandes d'Artisan](/docs/v3/doc/artisan/commands).

> **Note:** Si vous utilisez le mod_rewrite, vous devez définir dans l'option **index** une chaine de caractères vide.

<a name="Environnements"></a>
## Environnements

Souvent, les options de configurations que vous souhaitez pour votre environnement de développement ne sont pas les mêmes que les options pour la production. Laravel fourni un système de gestion d'environnements, qui se base par défaut sur les URL. Ouvrez le fichier `paths.php` qui se trouve à la racine de votre installation. Vous trouverez un tableau qui ressemble à cela : 

    $environments = array(

        'local' => array('http://localhost*', '*.dev'),

    );

Vous avez sans doute saisi le principe, cela indique au framework que toute les uls avec "http://localhost" ou finissant par ".dev" doivent être considéré comme étant dans l'environnement appellé "local".

Maintenant, créez un dossier **application/config/local**. Tous fichiers et toutes options qui se trouverons dans ce dossier écraseront les options de bases qui se situent dans le dossier de base **application/config** ; si vous êtes en environnement local. Par exemple, vous pourriez créer un fichier **application.php** avec votre configuration pour l'environnement **local** :

    return array(

        'url' => 'http://localhost/laravel/public',

    );

Dans cet exemple, l'option **url** de l'environnement local écrasera la valeur existante dans le fichier **application/config/application.php**. Notez que vous pouvez inscrire uniquement une partie des options, les autres prendront les valeurs par défaut.

Alors, plutôt simple non ? Bien sûr, vous pouvez créer autant d'environnement que vous le souhaitez !

<a name="cleaner-urls"></a>
## Des URLs propres

Vous ne souhaitez probablement pas que toutes les URLs de votre application contiennent "index.php". Vous pouvez supprimer ce comportement en utilisant des règles de réécritures HTTP. Si vous utilisez Apache en tant que serveur web, assurez vous que le mode rewrite soit activé, et créez un fichier **.htaccess** avec ce contenu dans le dossier **public** :

    <IfModule mod_rewrite.c>
         RewriteEngine on

         RewriteCond %{REQUEST_FILENAME} !-f
         RewriteCond %{REQUEST_FILENAME} !-d

         RewriteRule ^(.*)$ index.php/$1 [L]
    </IfModule>

Le fichier htaccess ne marche pas pour vous ? Essayez celui ci :

    Options +FollowSymLinks
    RewriteEngine on

    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d

    RewriteRule . index.php [L]

après avoir mis en place la réécriture HTTP, vous devrez mettre une chaine de caractères vide dans l'option **index** du fichier **application/config/application.php**.

> **Note:** Chaque serveur web gère differement les réécritures HTTP, le fichier htaccess peut alors être différent.
