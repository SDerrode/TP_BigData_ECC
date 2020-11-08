**Sommaire**

[TOC]


# _Spark streaming_


_Spark streaming_ ([_Spark streaming programming guide_](https://spark.apache.org/docs/1.5.0/streaming-programming-guide.html)) est une extension de la librairie principale de _Spark_, qui permet de traiter des flux continus de données. Elle est tolérante aux erreurs et permet de réaliser des algorithmes complexes grâce à des fonctions de haut niveau comme _map_, _reduce_, _join_, _window_. Finalement, les données traitées peuvent être sauvegardées sur différents systèmes de fichiers, dans des bases de données ou dans des tableaux de bord interactifs. Vous pouvez également appliquer des algorithmes _Spark_ de [Machine Learning](https://spark.apache.org/docs/1.5.0/mllib-guide.html) ou de [traitement de graphes](https://spark.apache.org/docs/1.5.0/graphx-programming-guide.html) sur les flux de données.

![streaming-arch](figures/streaming-arch.png)

_Spark Streaming_ reçoit les flux de données et les divise en paquets qui sont traités par le _Spark Engine_ pour générer le résultat sous forme de paquets.

![streaming-flow](figures/streaming-flow.png)

La librairie fournit des objets appelés `DStream`, pour _Discretized Stream_, qui représente un flux continu de données. Les `DStream` peuvent soit être créés par des flux de données entrants (HDFS), soit par des sources provenant de _Kafka_, _Flume_ ou _Kinesis_, ou encore par des opérations sur des `DStreams`. En interne, un `DStream` est représenté par une séquence de RDDs.

---
## _wordcount_ en _streaming_

Dans le _Namenode_, créez un nouveau répertoire et déplacez-vous dedans :
```bash
cd ..
mkdir sparkstreaming
cd sparkstreaming/
```
Depuis le second _Terminal_, copiez le fichier _SparkStreaming_wc.py_ dans le _Namenode_ :
```bash
docker cp SparkStreaming_wc.py hadoop-master:/root/sparkstreaming
```

Dans le premier _Terminal_, installez le serveur de données `netcat`
```bash
apt-get install netcat
```

Ouvrez un **troisième** _Terminal_, et entrez dans le _Namenode_ 
```bash
docker exec -it hadoop-master bash
```
Ainsi, si vous suivez bien, les _Terminaux_ 1 et 3 pointent tous deux sur le _Namenode_. Dans ce troisième _Terminal_, lancez le serveur de données `netcat` sur le port _9999_ de la manière suivante :
```bash
nc -l -p 9999
```
Dans le premier _Terminal_, lancez
```bash
spark-submit --master local[2] SparkStreaming_wc.py localhost 9999
```

Disposez les fenêtres des _Terminaux_ 1 et 3 côte à côte. Sur le _Terminal_ 3, tapez des mots rapidement, vous devriez voir le comptage de mot, chaque seconde, sur le _Terminal_ 1.

*Remarques* : pour entrer un série de mots d'un coup sur le _Terminal_ 3, vous pouvez soit 

  - écrire une ligne de mots séparés par des espaces. Envoyez alors la ligne d'un coup, en appuyant sur la touche `entrée` de votre clavier.
  - copier en mémoire (`CTRL+C` ou `CMD+C`) une ligne d'un texte quelconque, et la coller (`CTRL+V` ou `CMD+V`) dans le _Terminal_ 3.


Les paquets de données correspondent à une durée d'1 seconde. Pour allonger le temps associé aux paquets de données, il suffit de modifier la ligne `ssc = StreamingContext(sc, 1)`, en remplaçant la valeur 1 par la valeur souhaitée en secondes.