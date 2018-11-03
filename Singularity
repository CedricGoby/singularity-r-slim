bootstrap: docker
From: ubuntu:xenial

	# Texte affiché avec la commande
	# singularity help Ubuntu-16.04-R-slim.simg
%help
	Ubuntu-16.04-R-slim.simg est un container qui execute des scripts R et utilise SLiM
	
	La commande "Rscript" est executée au lancement du container (runscript).
	A la commande de lancement du container il faut donc ajouter comme argument le chemin (à l'intérieur du container) d'un script R
	qui sera lancé par "Rscript".
	Le script R peut lui aussi accepter des arguments.
	Exemple : singularity run Ubuntu-16.04-R-slim.simg /home/container/scripts/monscript.R --arg1 --arg2
	
	Lociciels installés :
	
	Ubuntu 16.04 LTS Xenial
	R version 3.4.4
	R est installé avec les packages suivants : hierfstat, poppr, inbreedR, genepop, abc, weights, abcrf, tree, hexbin, grid, quantregForest et plyr
	SLiM 2.6 : https://github.com/MesserLab/SLiM/releases/tag/v2.6
	
%setup

	# Commande executée au lancement du container
%runscript
    exec Rscript "$@"

	# Copie du fichier SLiM-2.6.tar.gz depuis l'hôte vers la racine du container
%files
	SLiM-2.6.tar.gz /

%environment

%labels
	AUTHOR cedric.goby@inra.fr

	# Commandes executées lors de la construction du container
%post
	# Création d'un dossier dans le container qui servira de point de montage
	mkdir -p /home/container/scripts
	
	# Mise à jour du système
	apt-get -y update && apt-get -y upgrade
	
	# Installation des paquets nécessaires aux installations ultérieures
	apt-get install -y apt-transport-https gnupg2 build-essential vim net-tools
	
	# Décompression de l'archive slim
	tar xvzf SLiM-2.6.tar.gz
	
	# Compilation de slim
	cd SLiM-2.6
	make slim
	
	# Déplacement de l'executable slim
	cd ..
	mv SLiM-2.6/bin/slim /usr/bin/
	
	# Suppression des fichiers et dossiers d'installation de slim
	rm -rf SLiM-2.6*
	
	## Ajout du dépôt R
	#echo "deb https://cloud.r-project.org/bin/linux/ubuntu xenial/" | tee /etc/apt/sources.list.d/r-project.list
	
	## Ajout de la clé publique du dépôt R
	#apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9
	
	## Mise à jour du système
	#apt-get -y update
	
	## Installation de R
	#apt-get install -y r-base r-base-dev
	
	## Installation de packages R
	#Rscript -e 'if (! require(hierfstat)) install.packages("hierfstat", repo="https://cran.rstudio.com/")'
	#Rscript -e 'if (! require(poppr)) install.packages("poppr", repo="https://cran.rstudio.com/")'
	#Rscript -e 'if (! require(inbreedR)) install.packages("inbreedR", repo="https://cran.rstudio.com/")'
	#Rscript -e 'if (! require(genepop)) install.packages("genepop", repo="https://cran.rstudio.com/")'
	#Rscript -e 'if (! require(abc)) install.packages("abc", repo="https://cran.rstudio.com/")'
	#Rscript -e 'if (! require(weights)) install.packages("weights", repo="https://cran.rstudio.com/")'
	#Rscript -e 'if (! require(abcrf)) install.packages("abcrf", repo="https://cran.rstudio.com/")'
	#Rscript -e 'if (! require(tree)) install.packages("tree", repo="https://cran.rstudio.com/")'
	#Rscript -e 'if (! require(hexbin)) install.packages("hexbin", repo="https://cran.rstudio.com/")'
	#Rscript -e 'if (! require(grid)) install.packages("grid", repo="https://cran.rstudio.com/")'
	#Rscript -e 'if (! require(quantregForest)) install.packages("quantregForest", repo="https://cran.rstudio.com/")'
	#Rscript -e 'if (! require(plyr)) install.packages("plyr", repo="https://cran.rstudio.com/")'

	# Test executé à la fin de la construction du container
%test
	cat /proc/version > software.versions
	slim -v
    #~ Rscript --version >> software.versions
	#~ R --version >> software.versions
	#~ Rscript -e 'installed.packages()' >> software.versions
