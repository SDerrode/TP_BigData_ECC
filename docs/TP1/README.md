# TP #1 - Linked Data

---
## Ressources

  - Client SPARQL [YASGUI](http://yasgui.triply.cc/)    
  - [Référence SPARQL](http://www.w3.org/TR/sparql11-query/)

---
## Travaux pratiques sur _DBPedia_

Le TP consiste à répondre aux 14 requêtes proposées ci-dessous, dans le [client Yasgui](https://yasgui.triply.cc).

### Quelques URIs utiles

  
  |---                                                        |---        |---                               |
  | [dbo:Person](http://dbpedia.org/ontology/Person)          | Classe    | Classe des personnes             |
  | [foaf:name](http://xmlns.com/foaf/0.1/Person)             | Propriété | Nom d'une personne (entre autre) |
  | [dbo:birthDate](http://dbpedia.org/ontology/birthDate)    | Propriété | Date de naissance d'une personne |
  | [dbo:birthPlace	](http://dbpedia.org/ontology/birthPlace) | Propriété | Lieu de naissance d'une personne |
  | [dbo:deathDate](http://dbpedia.org/ontology/deathDate)    | Propriété | Date de décès d'une personne     |
  | [dbo:deathPlace](http://dbpedia.org/ontology/deathPlace)  | Propriété | Lieu de décès d'une personne     |
  | [dbo:country](http://dbpedia.org/ontology/country)        | Propriété | Pays auquel un lieu appartient   |
  | [dbo:mayor](http://dbpedia.org/ontology/mayor)            | Propriété | Maire d'une ville                |
  | [dbr:Lyon](http://dbpedia.org/resource/Lyon)              | Instance  | La ville de Lyon                 |
  | [dbr:France](http://dbpedia.org/resource/Lyon)            | Instance  | La France                        |
  |--- 


### Quelques requêtes à programmer

  1. Afficher les URLs des lyonnais (_i.e._ personnes nées à Lyon)
  1. Afficher les URLs et les noms (`foaf:name`) des lyonnais
  1. Afficher les noms des lyonnais ne contenant pas de virgule (fonction `contains`)
  1. Afficher les noms (sans virgule) et dates de naissance des lyonnais
  1. Afficher les noms et dates de naissance des lyonnais nés après 1900 (`"1900"^^xsd:gYear`)
  1. Afficher les noms et dates de naissance des lyonnais nés après 1900 avec, le cas échéant, leur date de décès
  1. Afficher les noms de tous les lyonnais morts à Lyon
  1. Afficher les noms de tous les lyonnais morts hors de France
  1. Afficher toutes les villes françaises dont le maire est natif
  1. Afficher tous les maires français (_i.e._ d'une ville de France) nés hors de France
  1. Afficher tous les maires nés hors du pays où ils sont maires
  1. Afficher le nombre de maires français nés hors de France
  1. Afficher pour 10 villes françaises le nombre de natifs présents dans _DBPedia_
  1. Afficher les 10 villes ayant le plus de natifs dans _DBPedia_

Pour bien débuter, voici la réponse à la première requête, à savoir `Afficher les URLs des lyonnais (i.e. des personnes nées à Lyon)`:

```sparql
PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX dbr: <http://dbpedia.org/resource/>
SELECT ?p {
  ?p a              dbo:Person;
     dbo:birthPlace dbr:Lyon.
}
```