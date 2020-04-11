# Docker

Questo template è stato studiato per soddisfare i seguenti requisiti:

Un container backend con immagine ufficiale dockerhub php:7.3-fpm PHP versione 7.3 e Supervisor con comando php artisan queue:work

Un container frontend con immagine ufficiale dockerhub node:latest e angular CLI

Un container mysql con immagine ufficiale dockerhub mysql:latest

Un container phpmyadmin con immagine ufficiale dockerhub phpmyadmin/phpmyadmin, linkato al container mysql per poter accedere al DB 

Un container webserver con immagine ufficiale dockerhub nginx:alpine

## Init Docker


Il file /docker/backend/supervisor/supervisord.conf è linkato nel container backend. Modificando quel file viene replicato istantaneamente sul container

Prima installazione

Procedere con la copia del file .env.example per settaggio nome progetto ed utente da creare per DB mysql

`cp .env.example .env`

successivamente

`docker-compose  build`

Attendere che il tutto venga configurato

Successivamente:

`docker-compose  up -d`

Una volta che tutti i container sono inizializzati bisogna collegarsi sul container backend:

`docker exec -t -i backend /bin/bash`

ci ritroveremo già nella cartella /var/www/backend

Procedere con la copia del file .env.example ( è già settato il collegamento al database)

`cp .env.example .env`

installiamo tutte le dipendeze:

`composer install`

Per il backend non serve eseguire il comando php artisan serve in quanto il container nginx è linkato sulla cartella public

Per quanto riguarda il frontend ( Angular ) ho fatto in modo di esporre la 4200, in questo modo modificate il file in locale ma lo linka sulla docker instantaneamente e angular cli fa il resto sulla docker.

Quindi di seguito i link attualmente configurati:

backend: `localhost:8000`

frontend: `localhost:4200`

phpmyadmin: `localhost:7000`




