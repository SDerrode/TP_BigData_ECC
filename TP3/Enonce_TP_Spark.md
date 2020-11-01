**Sommaire**

[[_TOC_]]

# TP avec _Spark_ : Il est où le bel arbre ?

On considère ici le fichier de données [Opendata Paris](http://opendata.paris.fr), de type CSV, concernant des arbres remarquables à Paris. Ce fichier est disponible au [téléchargement](https://opendata.paris.fr/explore/dataset/arbresremarquablesparis/information/). Choisissez le menu `Export`et le format `csv`.

Copiez ce fichier dans le _Namenoe_ (`hadoop-master`). La commande 
```shell
more arbresremarquablesparis.csv
```
montre que chaque ligne décrit un arbre : 

  - position GPS, arrondissement, 
  - genre, espèce, famille, 
  - année de plantation, hauteur, circonférence, etc. 

Le séparateur entre les colonnes est le caractère ';'. La première ligne du fichier contient les titres des colonnes ; pour la supprimer, il suffit d'écrire:
```shell
sed '1d' arbresremarquablesparis.csv > arbresremarquablesparis2.csv 
```
Copiez alors _arbresremarquablesparis2.csv_ sur _HDFS_ (dans le répertoires `input`).


*Remarque :* 

  - Vous ne pouvez pas rédiger vos algo sur le _Namenode_ (il n'y a pas d'éditeur de texte). Éditez le fichier sur votre système d'exploitation, et envoyez-le sur le _Namenode_ par la commande `Docker cp ..`.


**Travail à faire** 

Écrivez des programmes _pyspark_ permettant 

  1. d'afficher les coordonnées GPS, la taille et l'adresse de l'arbre le plus grand.

    - Certains arbres n'ont pas de taille renseignée : on devra donc filtrer le RDD en supprimant les lignes dont la hauteur est égale à ''.       
    - La hauteur sera considérée comme une chaîne de caractères. Pour la transformer en nombre réel : `float(hauteur)`.     
    - Pour vérifier le résultat, vous pouvez utiliser [ce site](http://www.coordonnees-gps.fr/). Entrez les coordonnées GPS trouvées et vérifiez que l'adresse est bien la bonne !    
  2. d'afficher les coordonnées GPS des arbres de plus grande circonférence pour chaque arrondissement de la ville de Paris.
  3. d'afficher toutes les espèces d'arbre, triées par genre. 