# docker_tp01
# Exécuter un serveur web (apache, nginx, …) dans un conteneur docker
## a. Récupérer l’image sur le Docker Hub
  ```docker pull nginx```
## b. Vérifier que cette image est présente en local
  ```docker image ls```
## c. Créer un fichier index.html simple
## d. Démarrer un conteneur et servir la page html créée précédemment à l’aide d’un volume (option -v de docker run)
  ```docker run -d -p 80:80 -v /$(PWD):/usr/share/nginx/html nginx```
## e. Supprimer le conteneur précédent et arriver au même résultat que précédemment à l’aide de la commande docker cp
```docker run --name mynginx1 -p 80:80 -d nginx```
```docker cp ./ mynginx1:/usr/share/nginx/html```


# Builder une image
# a. A l’aide d’un Dockerfile, créer une image (commande docker build)
```docker build -t custom-nginx .```
```docker run -p 80:80 --name my-custom-nginx-container -d custom-nginx```
# b. Exécuter cette nouvelle image de manière à servir la page html (commande docker run)
# c. Quelles différences observez-vous entre les procédures 5. et 6. ? Avantages et inconvénients de l’une et de l’autre méthode ? (Mettre en relation ce qui est observé avec ce qui a été présenté pendant le cours) docker run -p 80:80 --name my-custom-nginx-container -d custom-nginx