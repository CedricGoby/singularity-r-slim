# singularity-R-slim

Construction d'un container Singularity avec Ubuntu, R et Slim pour du calcul à haute performance.

Le container exécute des scripts R et utilise SLiM

## Construction du container

Pour construire le container :

```
sudo singularity <nomducontainer>.simg Singularity
```

Le détail de la construction du container est commenté dans le fichier "Singularity"

## Utilisation du container

Dans l'exemple suivant on exécute le script R "/home/container/scripts/src/hello-world.R" 
en ayant au préalable monté le répertoire "scripts" dans le container. Le résultat du script est écrit dans "/home/container/scripts/results"

```
singularity run --bind /home/user/singularity-r-slim/scripts:/home/container/scripts <nomducontainer>.simg /home/container/scripts/src/hello-world.R
```