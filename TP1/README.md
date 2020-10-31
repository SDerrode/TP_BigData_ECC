# TP #1 - Linked Data

L'énoncé de ce TP est disponible à cette adresse : [TP _Linked data_](http://liris.cnrs.fr/%7Epchampin/2016/ecl-sparql/)  

Le TP consiste à répondre aux 14 requêtes proposées dans le [client Yasgui](https://yasgui.triply.cc) (selon la démonstration faite en fin de cours).

Pour bien débuter, voici la réponse à la première requête, à savoir ```Afficher les URLs des lyonnais (i.e. personnes nées à Lyon)```:

```sparql
PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX dbr: <http://dbpedia.org/resource/>
SELECT ?p {
  ?p a              dbo:Person;
     dbo:birthPlace dbr:Lyon.
}
```

Pour préparer ce TP, il vous est demandé de répondre aux requêtes #2 et #3 la semaine qui précède le début de la séance.
