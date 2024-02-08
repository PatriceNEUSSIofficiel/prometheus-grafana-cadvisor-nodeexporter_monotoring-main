# Documentation du TP D'inf 361

## MACHINE ADMINISTRATRICE:
 Je vais installé :
 - **OpenNMS** pour : 
  * Gestion Complète du Réseau : OpenNMS est une solution de gestion réseau complète qui couvre la collecte de données, la surveillance, la notification d'incidents, la cartographie réseau, et plus encore. Il offre une vue holistique de l'état du réseau.

  * Notification d'Incidents Sophistiquée : OpenNMS propose des fonctionnalités avancées de notification d'incidents, avec la possibilité de personnaliser les seuils, les escalades, et de définir des politiques de notification complexes

  * Topologie et Cartographie Réseau : Il génère des cartes interactives du réseau, permettant de visualiser la topologie, les connexions entre les dispositifs, et les performances globales du réseau.

  * Gestion des Utilisateurs et des Permissions :

    OpenNMS offre des fonctionnalités avancées de gestion des utilisateurs et des permissions, contrôlant l'accès aux données et aux fonctionnalités du système

- **Prometheus**:
  * pour la collecte, le stockage et la récupération des métriques de l'ensemble de l'environnement.

- - **CAdvisor** : il  sera responsable de la collecte de métriques spécifiques aux conteneurs, telles que l'utilisation CPU, la consommation de mémoire, le réseau. 

 Puis je vais configurer Prometheus pour récupérer les métriques exposées par cAdvisor. Prometheus a un support intégré pour la récupération de métriques à partir de cAdvisor.

- **Grafana** : Visualisation des métriques à l'aide de tableaux de bord.

## Machine administrée 

Je vais installé : 

 - **node_exporter** : collecter des métriques spécifiques au système hôte (CPU, mémoire, réseau, etc.)



   ### DEBUT DES CONFIGURATIONS :

   le workdir est : /home/patrice/docker-prometheus


   ### CREATION DU RESEAU :

   docker network create network_contenair 

   le pipeline est 

   #### LANCEMENT DES CONTENEURS
   
   **1** : Conteneur Manager : 
 - docker run -itd --privileged --name Manager  -v /var/run/docker.sock:/var/run/docker.sock -v /home/patrice/Desktop/INFOL3/admin/reseau/TP/docker-prometheus/Volume_Manager/:/home/patrice/Volume_Manager  --network=network_contenair docker sleep infinity
   
   **2** : Conteneurs Agents :
 - docker run -itd --privileged --name Agent1 -v /var/run/docker.sock:/var/run/docker.sock -v /home/patrice/Desktop/INFOL3/admin/reseau/TP/docker-prometheus/Volume_Agent1/:/home/patrice/Volume_Agent1  --network=network_contenair docker sleep infinity

  - docker run -itd --privileged --name Agent2  -v /var/run/docker.sock:/var/run/docker.sock -v /home/patrice/Desktop/INFOL3/admin/reseau/TP/docker-prometheus/Volume_Agent2/:/home/patrice/Volume_Agent2 --network=network_contenair docker sleep infinity

 - docker run -itd --privileged --name Agent3 -v /var/run/docker.sock:/var/run/docker.sock -v /home/patrice/Desktop/INFOL3/admin/reseau/TP/docker-prometheus/Volume_Agent3/:/home/patrice/Volume_Agent3 --network=network_contenair docker sleep infinity

     
#### Un Exec dans les conteneurs. 

* docker exec --workdir=/home/patrice/ --privileged -it Manager /bin/sh
* docker exec --workdir=/home/patrice/ --privileged -it Agent1 /bin/sh
* docker exec --workdir=/home/patrice/ --privileged -it Agent2 /bin/sh
* docker exec --workdir=/home/patrice/ --privileged -it Agent3 /bin/sh


##### executer le fichier docker-compose 

### DOnnez des addresses aux conteneurs: 
- creer un reseau à l'interieur : DinD
- leur connecter avec `docker network connect network_DinD nom_conteneur`

 docker network connect network_DinD grafana
 docker network connect network_DinD prometheus
 docker network connect network_DinD mycadvisor
 docker network connect network_DinD redis



