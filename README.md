# docker_tp01

# 5. Exécuter un serveur web (apache, nginx, …) dans un conteneur docker <br>
**a. Récupérer l’image sur le Docker Hub**<br>
  ```docker pull nginx```<br>
**b. Vérifier que cette image est présente en local**<br>
  ```docker image ls```<br>
**c. Créer un fichier index.html simple**<br>
**d. Démarrer un conteneur et servir la page html créée précédemment à l’aide d’un volume (option -v de docker run)**<br>
  ```docker run -d -p 80:80 -v /$(PWD):/usr/share/nginx/html nginx```<br>
**e. Supprimer le conteneur précédent et arriver au même résultat que précédemment à l’aide de la commande docker cp**<br>
```docker run --name mynginx1 -p 80:80 -d nginx```<br>
```docker cp ./ mynginx1:/usr/share/nginx/html```<br>

# 6. Builder une image<br>

**a. A l’aide d’un Dockerfile, créer une image (commande docker build)**<br>
```docker build -t custom-nginx .```<br>

**b. Exécuter cette nouvelle image de manière à servir la page html (commande docker run)**<br>
```docker run -p 80:80 --name my-custom-nginx-container -d custom-nginx```<br>

**c. Quelles différences observez-vous entre les procédures 5. et 6. ? Avantages et inconvénients de l’une et de l’autre méthode ? (Mettre en relation ce qui est observé avec ce qui a été présenté pendant le cours)**<br>

# 7. Utiliser une base de données dans un conteneur docker<br>

**a. Récupérer les images mysql:5.7 et phpmyadmin/phpmyadmin depuis le Docker Hub**<br>
``` docker pull mysql:5.7 ```<br>
``` docker pull phpmyadmin/phpmyadmin ```<br>

**b. Exécuter deux conteneurs à partir des images et ajouter une table ainsi que quelques enregistrements dans la base de données à l’aide de phpmyadmin**<br>
``` docker run --name db -e MYSQL_ROOT_PASSWORD=root -d mysql:5.7 ```<br>
``` docker run --name phpmyadmin -d --link db:db -p 8080:80 phpmyadmin/phpmyadmin ```<br>

# 8. Faire la même chose que précédemment en utilisant un fichier<br>

**a. Qu’apporte le fichier docker-compose par rapport aux commandes docker run ? Pourquoi est-il intéressant ? (cf. ce qui a été présenté pendant le cours)**<br>
```
Docker-compose permet de décrire la configuration d’un ou plusieurs services Docker ainsi que : leurs volumes et leurs réseaux
Il est intéréssant car il permet de gérer plusieurs conteneurs, faciliter le déploiement et la portabilité
```
<br>

**b. Quel moyen permet de configurer (premier utilisateur, première base de données, mot de passe root, …) facilement le conteneur mysql au lancement ?**<br>
``` Grâce au variable d'environnement définit par le "environment: " ```<br>

# 9. Observation de l’isolation réseau entre 3 conteneurs<br>

**a. A l’aide de docker-compose et de l’image praqma/network-multitool disponible sur le Docker Hub créer 3 services (web, app et db) et 2 réseaux (frontend et backend). Les services web et db ne devront pas pouvoir effectuer de ping de l’un vers l’autre**<br>


**b. Quelles lignes du résultat de la commande docker inspect justifient ce comportement ?**<br>
``` docker inspect <id_du_conteneur> ```<br>
``` La partie "Network" montre qu'ils sont dans un réseau différent les uns des autres. ```<br>

**c. Dans quelle situation réelles (avec quelles images) pourrait-on avoir cette configuration réseau ? Dans quel but ?**<br>
``` Cela permet de garder isoler le réseau de la DB pour une question de sécurité et pouvoir donner accès au front à l'extérieur. ```<br>