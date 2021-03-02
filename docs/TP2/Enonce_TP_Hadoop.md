**Sommaire**

[TOC]


# Travaux pratiques sous **Hadoop**

**Objectif du travail** : recueillir des informations et calculer des statistiques sur des résultats de ventes stockés dans le fichier _purchases.txt_. 


---
## Préparation et conseils

Dans le _bash_ du _Namenode_, déplacez-vous dans le dossier _ventes_ (à partir du premier _Terminal_) :
```bash
cd ../ventes
```
Les `..` permettent de remonter dans l'arborescence des dossiers d'un niveau (nous étions dans le répertoire _wordcount_). Pour observer le contenu du fichier présent dans ce dossier :
```bash
cat purchases.txt
```

Ainsi, vous pouvez constater que le fichier est organisé en 6 colonnes :

 - date (format `YYYY-MM-DD`);    
 - heure (format `hh:mm`);    
 - ville d'achat;    
 - catégorie de l'achat (parmi _Book_, _Men's Clothing_, _DVDs_...);    
 - somme dépensée par le client;    
 - moyen de paiement (parmi _Amex_, _Cash_, _MasterCard_...).

Les colonnes sont séparées par une tabulation. Ce caractère  est codé par _\t_ en _Python_. Exemple : `print("avant\tapres")` permet d'obtenir l'impression de la chaîne "_avant&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;apres_".

La commande _Linux_ `wc -l purchases.txt` permet d'obtenir le nombre de lignes du fichier (soit 4 138 476 lignes!). Ce fichier est sans doute trop volumineux pour régler vos algorithmes (le temps de debug en serait largement augmenté). Aussi, il est conseillé de travailler avec un extrait du fichier :
```bash
cat purchases.txt | head -n 100 > purchases_extrait100.txt
```
Cette commande extrait les 100 premières lignes du fichier et les stocke dans un fichier appelé _purchases_extrait100.txt_. N'oubliez cependant pas de vérifier vos scripts définitifs avec le fichier original.

Pensez à envoyer ces deux fichiers sur HDFS, dans le dossier _input_ :
```bash
hadoop fs -put purchases.txt input
hadoop fs -put purchases_extrait100.txt input
```

**Remarque** : Il n'est pas possible de programmer directement dans le _bash_ du _Namenode_, car celui-ci ne dispose pas d'éditeur de texte graphique (vous avez quand même accès à _vim_ et _nano_, mais en mode texte : essayez!). La solution consiste à 

 1. programmer vos scripts _map_ et _reduce_ avec votre IDE préférée (et pourquoi pas _Spyder_);    
 1. stocker vos fichiers (appelés _vente\_map.py_ et _vente\_reduce.py_) dans un dossier _vente_ que vous aurez créé sur votre machine (à côté du répertoire _wordcount_ de la première partie du TP ?);    
 1. envoyer vos 2 fichiers vers le _Namenode_ :
```bash
docker cp vente_map.py hadoop-master:/root/ventes
docker cp vente_reduce.py hadoop-master:/root/ventes
```
 
Avant de lancer le _job_ que vous aurez prévu dans les fichiers _vente_map.py_ et _vente_reduce.py_ avec la commande 
```bash
hadoop jar $STREAMINGJAR -input input/purchases_extrait100.txt -output sortie -mapper vente_map.py -reducer vente_reduce.py -file vente_map.py -file vente_reduce.py
``` 
dans le _bash_ du _Namenode_, pensez à rendre vos scripts exécutables :
```bash
chmod +x vente_map.py
chmod +x vente_reduce.py
```   
Vérifiez, avec la commande `cat vente_map.py`, que la première ligne du fichier est bien identique à :
```bash
#!/usr/bin/env python2.7
```   
Si non, alors corrigez le fichier en conséquence!    
Et si vous utilisez _Windows_, pensez également à convertir les fins de ligne de ces 2 fichiers avec `dos2unix`.

Vous êtes maintenant équipés pour développer les scripts _map-reduce_ permettant de répondre aux questions suivantes.

---
## Exercice - Questionner le fichier de ventes

Voici une liste de questions que vous pouvez aborder dans l'ordre (ou non!) :

 1. Quel est le nombre d'achats effectués pour chaque catégorie d'achat ?    
 1. Quelle est la somme totale dépensée pour chaque catégorie d'achat ?   
 1. Quelle somme est dépensée  dans la ville de _San Francisco_ dans chaque moyen de paiement ?
 1. Dans quelle ville la catégorie _Women's Clothing_ a permis de générer le plus d'argent _Cash_ ?
 1. À quelle heure les clients dépensent-ils le plus ? (type de réponse attendue : "entre 16h et 17h" par exemple)


Il est conseillé de développer un couple de fichiers différent pour chaque question (pour garder trace de vos algorithmes).


---
## Énoncé du CR de TP2

### Partie I

Il est conseillé de créer un nouveau répertoire pour réaliser cette partie :
```bash
cd ..
mkdir anagramme
cd anagramme
```

Étant donné un fichier de mots, écrire un script _map-reduce_ qui détecte les mots ayant **EXACTEMENT** les mêmes lettres (mais dans un ordre différent). 

Ainsi, par exemple, le fichier de mots suivant

> melon barre deviner lemon    
> arbre fiable fable vendre    
> devenir faible barbe

donnera en sortie cette liste:
   
> faible, fiable       
> arbre, barre    
> devenir, deviner    
> lemon, melon

La sortie ne devra afficher que les réponses avec aux moins 2 mots. Dans cet exemple, les mots `fable` ou `barbe` n'apparaissent pas car ce sont les seuls mots de la liste avec ces lettres.

Pour vos tests, vous pourrez utiliser le fichier de mots suivant : 
```bash
wget https://raw.githubusercontent.com/dwyl/english-words/master/words_alpha.txt
```

Cet algorithme devra fonctionné sous environnement _Hadoop_, avec plusieurs _mapper_ et _reducer_ en parallèle. L'algorithme ne devra pas tenir compte de la présence éventuelle de majuscules dans les mots.

### Partie II

Proposez une **requête originale et complexe** sur le fichier de ventes. Dans le CR, veuillez:

 - Décrite la requête en quelques phrases, et montrer le résultat obtenu (ou un extrait si trop volumineux).
 - Inclure le code de la requête dans le zip.
