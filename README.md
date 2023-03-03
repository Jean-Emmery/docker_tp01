# docker_tp01

# 5. Exécuter un serveur web (apache, nginx, …) dans un conteneur docker
**a. Récupérer l’image sur le Docker Hub**
  ```docker pull nginx```
**b. Vérifier que cette image est présente en local**
  ```docker image ls```
**c. Créer un fichier index.html simple**
**d. Démarrer un conteneur et servir la page html créée précédemment à l’aide d’un volume (option -v de docker run)**
  ```docker run -d -p 80:80 -v /$(PWD):/usr/share/nginx/html nginx```
**e. Supprimer le conteneur précédent et arriver au même résultat que précédemment à l’aide de la commande docker cp**
```docker run --name mynginx1 -p 80:80 -d nginx```
```docker cp ./ mynginx1:/usr/share/nginx/html```

# 6. Builder une image

**a. A l’aide d’un Dockerfile, créer une image (commande docker build)**
```docker build -t custom-nginx .```

**b. Exécuter cette nouvelle image de manière à servir la page html (commande docker run)**
```docker run -p 80:80 --name my-custom-nginx-container -d custom-nginx```

**c. Quelles différences observez-vous entre les procédures 5. et 6. ? Avantages et inconvénients de l’une et de l’autre méthode ? (Mettre en relation ce qui est observé avec ce qui a été présenté pendant le cours)**

# 7. Utiliser une base de données dans un conteneur docker

**a. Récupérer les images mysql:5.7 et phpmyadmin/phpmyadmin depuis le Docker Hub**
``` docker pull mysql:5.7 ```
``` docker pull phpmyadmin/phpmyadmin ```

**b. Exécuter deux conteneurs à partir des images et ajouter une table ainsi que quelques enregistrements dans la base de données à l’aide de phpmyadmin**
``` docker run --name db -e MYSQL_ROOT_PASSWORD=root -d mysql:5.7 ```
``` docker run --name phpmyadmin -d --link db:db -p 8080:80 phpmyadmin/phpmyadmin ```

# 8. Faire la même chose que précédemment en utilisant un fichier

**a. Qu’apporte le fichier docker-compose par rapport aux commandes docker run ? Pourquoi est-il intéressant ? (cf. ce qui a été présenté pendant le cours)**
```
- Docker-compose permet de décrire la configuration d’un ou plusieurs services Docker ainsi que : leurs volumes et leurs réseaux
Il est intéréssant car il permet de gérer plusieurs conteneurs, faciliter le déploiement et la portabilité
```

**b. Quel moyen permet de configurer (premier utilisateur, première base de données, mot de passe root, …) facilement le conteneur mysql au lancement ?**
``` Grâce au variable d'environnement définit par le "environment: " ```

# 9. Observation de l’isolation réseau entre 3 conteneurs

**a. A l’aide de docker-compose et de l’image praqma/network-multitool disponible sur le Docker Hub créer 3 services (web, app et db) et 2 réseaux (frontend et backend). Les services web et db ne devront pas pouvoir effectuer de ping de l’un vers l’autre**


**b. Quelles lignes du résultat de la commande docker inspect justifient ce comportement ?**
``` docker inspect "id_du_conteneur"```
``` La partie "Network" montre qu'ils sont dans un réseau différent les uns des autres. ```

**c. Dans quelle situation réelles (avec quelles images) pourrait-on avoir cette configuration réseau ? Dans quel but ?**
``` Cela permet de garder isoler le réseau de la DB pour une question de sécurité et pouvoir donner accès au front à l'extérieur. ```