# Installation PHP/Mcrypt on MacOSX Mavericks (10.9) 


#### Installer l'outils ligne de commande d'Xcode

- xcode-select --install

Lorsque l'installation est terminé, passons à la récupération de PHP ainsi que de l'extension MCrypt.

Vous devez récupérer VOTRE version de PHP sur le site php.net

Sur mon environnement à l'heure ou j'écrit cette aide est : 

> PHP 5.4.17 (cli) (built: Sep 12 2013 23:14:23)

> Copyright (c) 1997-2013 The PHP Group

> Zend Engine v2.4.0, Copyright (c) 1998-2013 Zend Technologies

Vous pouvez récupérer l'identifiant de version en tapant :

- php -v

#### PHP et MCrypt

Télécharger : 

- [libmcrypt 2.5.8](http://downloads.sourceforge.net/project/mcrypt/Libmcrypt/2.5.8/libmcrypt-2.5.8.tar.gz?r=http%3A%2F%2Fsourceforge.net%2Fprojects%2Fmcrypt%2Ffiles%2FLibmcrypt%2F2.5.8%2F&ts=1388326033&use_mirror=freefr)

- [php-5.4.17](http://museum.php.net/php5/php-5.4.17.tar.gz)


Nous allons créer un dossier mcrypt et y placer les téléchargement :

- cd ~
- mkdir mcrypt
- cd mcrypt
- tar -xvzf libmcrypt-2.5.8.tar.gz
- tar -xvzf php-5.4.17.tar.gz
- rm *.gz

Voila, notre dossier est prêt, nous allons donc commencer l'execution.

#### Configuration de la librairie MCrypt

- cd libmcrypt-2.5.8
- ./configure
- make
- sudo make install
-
La librairie est maintenant configurée, il est temps de créer l'extension.

#### Errors Autoconf

J'ai eu cette erreur sur deux Mac différent, j'installe donc ceci à chaque fois.

- cd ~/mcrypt
- curl -O http://ftp.gnu.org/gnu/autoconf/autoconf-latest.tar.gz
- tar xvfz autoconf-latest.tar.gz
- cd autoconf-2.69/
- ./configure
- make
- sudo make install

#### Compilation MCrypt PHP
A présent nous allons compiler mcrypt et vérifier que tout ce passe bien.

- cd ~/mcrypt/php-5.4.17/ext/mcrypt/
- /usr/bin/phpize

La commande précédente devrai vous afficher quelques choses comme ceci : 

> Configuring for:

> PHP Api Version:         20100412

> Zend Module Api No:      20100525

> Zend Extension Api No:   220100525

Executer donc les commandes suivantes :

- ./configure
- make
- sudo make install

#### Configuration de PHP
De base le fichier php.ini n'est présent que sous forme de fichier par defaut, nous allons tout d'abord le récupérer.

- sudo cp /etc/php.ini.default /etc/php.ini

Ensuite ajouter dans ce fichier la ligne suivante via vim ou nano par exemple. 

- extension=mcrypt.so

Effectuer un redemarrage d'apache afin de finir l'installation

- sudo apachectl restart


Voila, tout devrais fonctionner correctement désormais.