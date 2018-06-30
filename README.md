[![Build Status](https://travis-ci.com/dbjpanda/drupal-on-docker.svg?token=55CADUHzgmryMHLpbyAs&branch=master)](https://travis-ci.com/dbjpanda/drupal-on-docker)

Optional steps but recommended
----------------------
Install Traefik to access your Drupal site using their "domain name" instead of "IP:port" . This is an one time setup and use with all projects. This is usefull for both Drupal and Non-Drupal projects.
```$xslt
docker network create -d bridge traefik-network
docker run -d --network=traefik-network -p 80:80 -p 8080:8080 -v /var/run/docker.sock:/var/run/docker.sock --name=traefik traefik:latest --api --docker
```

Installation of Drupal on development server
----------------------
Step 1
``````
git clone https://github.com/ankitjain28may/affiliates-connect.git
```````
Step 2 (optional)
````````
Modify .env file as per your requirements
``````````````
Step 3
````````
docker-compose up -d
````````

Step 4
````````
docker exec -it PROJECT_NAME composer install
````````

Step 5 (Import configuration)
````````
docker exec -it PROJECT_NAME vendor/bin/drupal ci
````````

Step 6 (Rebuild Cache)
````````
docker exec -it PROJECT_NAME vendor/bin/drupal cr
````````


Installation of Drupal on production server
---------------------------
Here you need to override the default environment variables for production server. You can achieve it by below command while deploying.

````````
SITE_NAME=example.com MYSQL_USER=someone MYSQL_PASS=yoursecrets docker-compose up -d
``````````````

Login in Drupal using below credentials
----------------------
username - admin

password - aaaaaa

Set up Advance feeds crawler config
----------------------
1. Go to configuration page, Under 'System' block, click Advance Crawler Settings
2. Enter the Nodejs Server host -
  If you are running on your localhost, then enter local ip like `192.168.*.*`
  localhost wont work as docker will search for the address inside the container.
3. Enter the Nodejs server port
