**Sommaire**

[TOC]

# Wordcount, en local

Nous allons ici faire fonctionner l'algorithme _map-reduce_ qui compte les mots d'un fichier texte, en local, _i.e._ sans exploiter le parallélisme que propose le framework **Hadoop**. Le programme est constitué de deux scripts _Python_ qui sont appelés successivement selon la méthode décrite ci-dessous. Il s'agit ici surtout de comprendre la logique algorithmique.


---
## Récupération et lancement des scripts _Python_

Pour récupérer le scripts, suivez les consignes:

  - Ouvrez un _Terminal_ et déplacez-vous dans votre dossier de travail (avec la commande ```cd```). Tapez la commande permettant de récupérer les fichiers nécessaires à ce TP.   
```bash
git clone https://gitlab.ec-lyon.fr/sderrode/TP_BigData_ECL.git
```
  Constatez, dans un gestionnaire de fichiers, que cette commande a permis de rapatrier des fichiers répartis dans 2 dossiers : _TP\_Hadoop_ et _TP\_SparQL_. Nous allons ici travailler sur le dossier _TP\_Hadoop_.

  - Dans le _Terminal_, déplacez-vous dans le dossier _wordcount_, en lançant successivement les 3 commandes suivantes :
```bash
cd TP_BigData_ECL
cd TP_Hadoop
cd wordcount
```
  ou plus simplement :    
```bash
cd TP_BigData_ECL/TP_Hadoop/wordcount
```

  La commande ```ls``` permet de lister le contenu du dossier. Vous pouvez observer la présence des 2 fichiers _mapper.py_ et _reducer.py_, ainsi que du livre _Dracula_ (libre de droit. Ce dernier peut être téléchargé depuis [cette adresse](http://www.textfiles.com/etext/FICTION/dracula), ou en exécutant, depuis un _Terminal_, la commande 
```bash
wget http://www.textfiles.com/etext/FICTION/dracula
```  

  - Lancez la commande suivante et observez le résultat:
```bash
cat dracula | python mapper.py
```
  *Remarque* Si vous utilisez _Windows_, remplacer `python` par `python.exe`. Pensez à faire ce changement partout dans l'énoncé.

  - Lancez ensuite la commande entière et observez le résultat:
```bash
cat dracula | python mapper.py | sort | python reducer.py 
```

**Remarque Windows** Pour les étudiants utilisant _Windows_, vous pourriez rencontrer des difficultés avec les 2 lignes suivantes, qui font appel à _Python_ en ligne de commandes. La raison : l'endroit où est stocké le programme _python.exe_ n'est pas connu de votre machine, il faut donc le préciser en modifiant la variable d'environnement _PATH_. Pour cela, vous pouvez suivre les indications données dans la Section _Method 2: Manually add Python to Windows Path_ de [ce lien](https://datatofish.com/add-python-to-windows-path/).

**Remarque importante** La première ligne de tous vos scripts _Python_ devra être
```bash
#!/usr/bin/env python2.7
```
Cette ligne indique que si le script doit être exécuté, alors c'est avec _python2.7_ qu'il doit l'être.

----
## Exercice 1 - Amélioration du *wordcount*

*Remarque* : Pour stocker le résultat d'exécution du script dans un fichier appelé _result.txt_, on lancera
```bash
cat dracula | python mapper.py | sort | python reducer.py > results.txt
```

Ouvrez ce fichier avec votre éditeur de texte préféré, et regardez les premières lignes. On constate de nombreux problèmes :

  - la présence de signes de ponctuation dans les mots;
  - les mots commençant par une majuscule sont distingués des mots commençant par une minuscule. 

Pour régler ces problèmes, veuillez

  1. Modifier les scripts _Python_ précédents pour qu'ils ne distinguent plus les mots qui comportent des majuscules et les mêmes mots qui n'en comportent pas.    
  1. Modifier la version précédente, de telle manière que les signes de ponctuation ne soient plus pris en compte (consultez Internet pour trouver un moyen de supprimer les signes de ponctuation d'une chaîne de caractères représentant un mot).
