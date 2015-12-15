# tutoriel-script-bash
##Tous nos tutoriels HTML since 10/2015


######créé par David TARCZEWSKI @david

un petit tutoriel *à améliorer* pour faire ses **scripts bash** et automatiser les tâches répétitives sur son système

1. Pourquoi ?
  11. Besoins
  12. Exemple
2. Comment ?
  21. Nommage
  22. Droits
  23. Appel
3. Exercice


##Pourquoi avoir besoin d'écrire un script ?

###Besoins
* Chaque fois que l'on sait que les commandes tapées vont nous servir plusieurs fois...
* Par exemple, faire des copies de sauvegarde d'un ou plusieurs dossiers et/ou fichiers dans un endroit sécurisé.

###Exemples

Voici un exemple de script :

```
#!/bin/bash

rsync -av --partial --progress --stats --bwlimit=20 /home/user/l-espace-a-sauvegarder/ /la/destination/de/sauvegarde/

exit 0
```

Ici on donne la commande rsync

en paramètre on indique :
- `-a` pour archive
- `-v` pour verbose
- `--partial` pour conserver les fichiers partiellement transférés si on doit arrêter puis reprendre la commande plus tard...
- `--progress` pour afficher une petite barre de progression
- `--stats` pour afficher les statistiques de transfert à la fin
- `--bwlimit=nn` le taux de transfert souhaité en kb par secondes
- ensuite le dossier de départ, puis le dossier de destination...

On peut créer une archive = .tar , en précisant entre guillemets les chemins absolus des dossiers à sauvegarder.

```
tar -cvzf /media/utilisateur/USB-STICK/backup.tar.gz "/home/utilisateur/simplon/" "/var/www/" "/usr/local"
```

##Comment ?

###Nommage :

Ce fichier que l'on créé, on lui donne un nom qui porte l'extension (se termine) .sh , par exemple save.sh.

Il faut préciser en premier le langage utilisé dans notre cas : `bash`.
Ça s'écrit : `#!/bin/bash`
Et on le déclare en première ligne.

###Droits :

Il faut qu'il soit exécutable. 
Pour vérifier cela, faire un ls -l. 

```
-rwxr-xr-x 1 david david  743 nov.   5 14:01 save.sh
```

- le - = fichier,
- ensuite 3 signes : droits de l'utilisateur,
- puis 3 autres signes : droits du groupe,
- puis encore 3 signes : droits des autres.
- ensuite le nom de l'utilisateur, et celui du groupe qui ont les droits précédemment indiqués...

S'il ne l'est pas, taper en console :

```
$sudo chmod u+x save.sh
```


###Appel :

Pour l'appeler il faut se placer à l'endroit où il se trouve, puis taper en console `./` avant son nom, par exemple `$./save.sh`

Il est possible de pouvoir l'appeler depuis n'importe où, en le plaçant simplement dans un répertoire que l'on nommera `bin` dans son `/home` ...
Puis de dire au système que ce `/home/utilisateur/bin` fait partie du `$PATH` 

```
$cd
$mkdir bin
$mv /chemin/du/save.sh bin/
$echo $PATH
$export PATH=$PATH:$HOME/bin
$save.sh
```

##EXERCICE :

- Créez un dossier de test nommé testscript
- Placez vous dedans
- Créer 2 fichier : fichier1 et fichier2
- dans fichier 1 écrivez quelque chose
- Créez un script bash(scriptsynchro.sh) qui va synchoniser fichier1 avec fichier2
- Une fois fait, vérifiez-en les droits et donnez lui les droits d'exécution pour tout le monde
- Exécutez-le en observant bien votre console
- Rendez-le maintenant exécutable de n'importe où... (vérifier le $PATH et si nécessaire indiquez-lui où trouver votre répertoire bin)

