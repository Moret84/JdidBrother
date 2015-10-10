# JdidBrother

Ce script est un script de surveillance des cours de la bourse de Paris.  
Pour qu'il fonctionne, il est nécéssaire de conserver l'aborescence du dossier dans lequel se trouve le fichier que vous êtes actuellement en train de lire.  
Cette arborescence se compose de quatre dossiers :  

1. Un dossier config, dans lequel on trouvera tous ce qui est nécéssaire à la configuration du script, à savoir les fichiers suivants :  
	1. Le fichier config/companiesList.conf, qui est le fichier qui contient les noms des entreprises qu'il est possible de suivre en utilisant le script, auxquelles sont associés leur symbole boursier.  
	2. Le fichier config/help.conf, contenant l'aide du programme.  
	Au cours de l'utilisation du script, le dossier config se garnit de fichiers supplémentaires :  
	3. Le fichier config/watchList.conf, qui va contenir la liste des symboles boursiers des entreprises configurées comme à surveiller.  
	4. Le fichier config/settings.conf, contenant tous les réglages inhérents à l'exécution automatique du script.  

2. Un dossier data, contenant les données + graphiques, un sous dossier par entreprise à surveiller, chaque sous-dossier contient:  
	1. Un fichier prices.dat, qui contient tous les cours de l'entreprise, précédé de la date de ce prix, le plus récent étant en bas.  
	2. Les graphiques représentant les cours en fonction du temps . Ces graphiques possèdent le masque de nom JJMMYYYY_HHMMSS.png .  

3. Un dossier saves, qui est l'emplacement par défaut des sauvegardes des graphiques, et contenant les fichiers de sauvegarde, nommé selon le masque Save_JJMMYYYY_HHMMSS.tar  

4. Un dossier src, qui contient les 8 fichiers contenant les définitions des fonctions utilisées dans le script :  
	* add  
	* remove  
	* configure  
	* start  
	* stop  
	* pull  
	* draw  
	* save  

Ces fonctions sont documentées ci après :  

##### fonction add :  

Prend en paramètre(s) le(s) nom(s) de l' (des) entreprise(s) que l'on veut ajouter à la surveillance, ces noms doivent être tels que dans le fichier config/companiesList.conf sinon un message d'erreur est affiché.  
En cas de succès, la fonction le signale et ajoute dans le fichier config/watchList.conf les symboles boursiers de l' (des) entreprise(s) donnée(s) en paramètre(s).  
S'il y a doublon, l'entreprise n'est pas ajoutée et un message d'erreur est affichée.  


##### fonction remove :  

Retire de la liste config/watchList.conf les symboles fiscaux des entreprises passées en paramètres, ceci afin de les retirer de la surveillance.  
Si l'entreprise n'est pas dans la liste, un message est affiché.  


###### fonction configure :  

Lance le script de configuration du fonctionnement automatique du script.  
Cette fonction demande à l'utilisateur les intervalles de temps qu'il souhaite pour respectivement la récupération automatique de données, le dessin de nouveaux graphes, et la sauvegarde des graphes.   
Elle demande pareillement le taux critique de baisse d'une action en dessous duquel on souhaite être averti par mail, ainsi que l'adresse mail à laquelle on souhaite être averti.  
Enfin, sont également demandé le nombre de graphiques à garder (x derniers) lors de la sauvegarde ainsi que le dossier de sauvegarde.  
Le fichier config/settings.conf est créé avec pour contenu ces informations.  


##### fonction start :  

Démarre le script en ajoutant dans la crontab les informations données lors de la configuration ainsi que les fonctions pull, draw et save.  
Si l'ajout dans la crontab échoue, un message d'erreur est affiché.  

##### fonction stop :  
Arrête le script en le retirant de la crontab.  
Si le script n'est pas dans la crontab, la fonction ne fait rien et signale que le script n'est pas en marche.  


##### fonction pull :  
Lance la récupération de nouvelles informations sur les cours des actions de chacune des entreprises surveillées.  
Avertit l'utilisateur d'une baisse supérieure au seuil qu'il a fixé (sous réserve que le client mail en ligne de commande soit correctement configuré).  

##### fonction draw :  
Trace des graphiques basées sur les données de prix pour chacune des entreprises surveillées.  


##### fonction save :  
Sauvegarde les graphiques en utilisant les informations configurées.  


Pour utiliser le script, lancez simplement la commande JdidBrother depuis le répertoire où il se trouve.  
Apparaît alors un petit menu vous présentant les 8 fonctions que vous pouvez utiliser, avec une petite explication pour chacune.
L'intégralité du script a été rédigée en anglais.   
Pour utiliser une des 8 fonctions, entrez simplement son nom précédé du nom du script JdidBrother.  
Par exemple, pour utiliser la fonction add, tapez simplement JdidBrother add depuis le répertoire où se trouve le script principal.  
Pour plus d'informations, lire la documentation ci-dessus et/ou utiliser la commande JdidBrother help.  
