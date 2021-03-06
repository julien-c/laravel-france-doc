# Erreurs & Logging

## Au menu

- [Configuration basique](#basic-configuration)
- [Logging](#logging)
- [La classe Logger](#the-logger-class)

<a name="basic-configuration"></a>
## Configuration basique

Toutes les options de configuration qui concerne les erreurs et le logging se trouvent dans le fichier **application/config/errors.php**. Jetons y un oeil.

### Erreurs ignorées

L'option **ignore** contient un tableau des niveaux d'erreurs qui voient être ignorés par Laravel. Par "ignoré", nous voulons dire que nous n'arreterons pas l'execution d'un script pour ces erreurs. Cependant, elles seront logguées si le logging est activé.

### Détails d'erreurs

L'option détail **detail** indique si le framework doit afficher le messge d'erreur et la pile de suivie quand une erreur se produit. En développement, vous pouvez le mettre à **true**, cependant production, placez celà à **false**. Lorsqu'il est à false, la vue située dans le fichier **application/views/error/500.php** sera affichée. Elle contient un message d'erreur générique.

<a name="logging"></a>
## Logging

Pour activer le logging, placez l'option **log** à true dans le fichier de configuration **errors.php**. Quand le loggine est actif, la fonction anonyme contenue dans l'élément **logger** du fichier de configuration sera executé lorsqu'une erreur surgie. Cela vous donne une flexibilité totale sur la manière dont les erreurs doivent être logguées. Vous pouvez par exemple envoyé un email à l'équipe de développement !

Par defaut, les fichiers de logs sont stockés dans le répertoire **storage/logs**, et un nouveau fichier de log est créé chaque jours. Cela empêche d'avoir de gros fichiers de logs avec trop de messages.

<a name="the-logger-class"></a>
## La classe Logger

Vous pouvez si vous le souhaitez utiliser la classe **Log** de Laravel pour debugguer, ou juste logguer des messages d'informations. Voici comment l'utiliser :

#### Ecriture d'un message dans le log :

	Log::write('info', 'Ceci est un message informel');

#### Utilisation de la méthode magique pour spécifier le type de message:

	Log::info('Ceci est un message informel');