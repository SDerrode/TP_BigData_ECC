**Sommaire**

[TOC]


# Tests de _Spark_, avec la librairie _pyspark_

Nous allons ici faire fonctionner l'algorithme de comptage de mot, mais rédigé avec _pyspsark_, la librairie _Python_ qui permet de programmer _Spark_.

----
## Relancer le cluster

Il faut dans un premier temps, relancez le cluster que nous avions installé pour _Hadoop map-reduce_, avec son _Namenode_ et ses deux _Datanodes_. Tout d'abord, lancer `Docker Desktop`. Puis, dans un premier _Terminal_, tapez :
```shell
docker start hadoop-master hadoop-slave1 hadoop-slave2
```
Puis entrez dans le shell du _Namenode_ :
```shell
docker exec -it hadoop-master bash
```
Lancez alors le _daemon hadoop_ :
```shell
./start-hadoop.sh
```
Vérifiez alors que _HDFS_ est bien monté, avec la commande :
```shell
hadoop fs -ls
```

----
## _wordcount_ en Spark

Entrez dans le répertoire _wordcount_, listez les fichiers contenus dans ce répertoire :
```shell
cd wordcount
ls
```
Il s'agit des scripts python _Hadoop_ du [TP2](./TP2). Nous allons maintenant importer le même programme mais rédigé en _pyspark_ (ie. _Spark_ pour _Python_). Depuis un second _Terminal_, ouvert dans le répertoire où vous avez téléchargé le contenu du répertoire _scripts_, tapez la commande
```shell
docker cp PySpark_wc.py hadoop-master:/root/wordcount
```
Revenez au premier _Terminal_, et vérifiez que le fichier est là où il est attendu !

Avant de lancer le script, il convient de vérifier que le répertoire _sortie_ n'existe pas déjà sous _HDFS_. Pour faire cela, on tente de l'effacer (qu'il existe ou non !) :
```shell
hadoop fs -rm -r -f sortie
```
et il convient de faire connaître à _Spark_ la version de _Python_ à utiliser, à travers une variable d'environnement :
```shell
export PYSPARK_PYTHON=python2.7
```

Ensuite, lancez le comptage de mots sur le livre _dracula_, en local, avec 2 cœurs de votre processeur : 
```shell
spark-submit --master local[2] PySpark_wc.py input/dracula
```
Pour vérifier le résultat, scruter le contenu du répertoire _sortie_ sou _HDFS_ :
```shell
dfs dfs –ls sortie
```
et le contenu des deux fichiers de sortie
```shell
hdfs dfs –text sortie/part-00000
hdfs dfs –text sortie/part-00001
```

**Travail à faire** Faites évoluer la version précédente de telle manière que l'on ne garde que les mots qui apparaissent dans le texte au moins _X_ fois, la valeur de _X_ étant fixée par un argument supplémentaire lors de l’appel à `spark-submit`. Par exemple :
```shell
spark-submit --master local[2] PySpark_wc.py input/dracula 1000
```

----
## Tester les scripts du cours

D'abord, créez et entrez dans un nouveau répertoire, à la racine de votre compte :
```shell
cd ..          # pour remonter d'un  niveau de répertoire dans l'arborescence
mkdir pyspark
cd pyspark
```

Dans le second _Terminal_, rapatriez l'ensemble des scripts _PySpark_ex*.py_ dans le répertoire que nous venons de créer :
```shell
for f in PySpark_ex*.py; do docker cp $f hadoop-master:/root/pyspark; done
```
et rapatriez également le programme qui donne une approximation de _pi_ :
```shell
docker cp PySpark_Pi.py hadoop-master:/root/pyspark
```

*Remarque* Pour le script _PySpark_exemple5.py_, vous aurez besoin du fichier _baby_names_2013.csv_, que j'ai mis à votre disposition dans le même répertoire que ce fichier. N'oubliez pas de le déposer sur _HDFS_ avant de lancer le script (vous savez comment faire maintenant...).