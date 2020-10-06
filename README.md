# Comment installer Wordpress avec Docker

- Installer le logiciel Docker
- Créer un compte Docker et connecter Docker Desktop
- Créer un nouveau projet dans PHPStorm
- Copier le fichier docker-compose.yml dans ce dossier
- Ouvrir le terminal (en bas de la fenêtre, dans PHPStorm)
- Lancer la commande ```docker-compose up -d``` et attendre le téléchargement
- En cas d'erreur, est-ce que le port n'est pas déjà utilisé ?
- Après quelques secondes, le container est lancé, ouvrir le navigateur à l'adresse [http://localhost:8000](http://localhost:8000)
- Installer Wordpress en prenant soin de ne pas perdre l'identifiant et le mot de passe
- Se connecter au backoffice de Wordpress [http://localhost:8000/wp-admin/](http://localhost:8000/wp-admin/)
- Installer l'extension **All In One WP Migration** et l'activer
- Modifier les paramètres de limite de téléchargement en ajoutant le code dans le fichier ```.htaccess```
- Importer l'archive du site
- Se reconnecter avec le login fourni ("stagiaire")
- Enregistrer les permaliens

Et c'est parti, ça roule...

Fichier docker-compose.yml :

```yml
version: '3.3'

services:
   db:
     image: mysql:5.7
     volumes:
       - db_data:/var/lib/mysql
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: somewordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress

   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     ports:
       - "8000:80"
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: wordpress
       WORDPRESS_DB_PASSWORD: wordpress
       WORDPRESS_DB_NAME: wordpress
     volumes:
       - ./wordpress:/var/www/html

volumes:
  db_data: {}
```
