[TOC]

# TP Linked Data

La première partie du TP consiste à répondre aux requêtes sur la base _linked data_ appelée _DBPédia_. La seconde partie consiste à imaginer 2 requêtes originales sur l'une des bases listées. Seule cette seconde partie devra faire l'objet d'un compte-rendu.

Voici une référence sur le [langage SPARQL](http://www.w3.org/TR/sparql11-query/).

---
## Travaux pratiques sur _DBPedia_

Répondez aux 14 requêtes proposées ci-dessous dans le [client Yasgui](https://yasgui.triply.cc). 

### Quelques URIs utiles

|                                                           |           |                                  |
| ---                                                       | ---       | ---                              |
| [foaf:Person](http://xmlns.com/foaf/0.1/Person)           | Classe    | Classe des personnes             |
| [foaf:name](http://xmlns.com/foaf/0.1/name)               | Propriété | Nom d'une personne (entre autre) |
| [dbo:birthDate](http://dbpedia.org/ontology/birthDate)    | Propriété | Date de naissance d'une personne |
| [dbo:birthPlace	](http://dbpedia.org/ontology/birthPlace) | Propriété | Lieu de naissance d'une personne |
| [dbo:deathDate](http://dbpedia.org/ontology/deathDate)    | Propriété | Date de décès d'une personne     |
| [dbo:deathPlace](http://dbpedia.org/ontology/deathPlace)  | Propriété | Lieu de décès d'une personne     |
| [dbo:City](http://dbpedia.org/ontology/city)              | Propriété | Ville                            |
| [dbo:country](http://dbpedia.org/ontology/country)        | Propriété | Pays auquel un lieu appartient   |
| [dbo:mayor](http://dbpedia.org/ontology/mayor)            | Propriété | Maire d'une ville                |
| [dbr:Lyon](http://dbpedia.org/resource/Lyon)              | Instance  | La ville de Lyon                 |
| [dbr:France](http://dbpedia.org/resource/France)          | Instance  | La France                        |


### Quelques requêtes à programmer

  1. Afficher les URLs des lyonnais (_i.e._ personnes nées à Lyon). La réponse à cette requête est présentée ci-dessous.
  1. Afficher les URLs et les noms (`foaf:name`) des lyonnais.
  1. Afficher les noms des lyonnais ne contenant pas de virgule (fonction `contains`).
  1. Afficher les noms (sans virgule) et dates de naissance des lyonnais.
  1. Afficher les noms et dates de naissance des lyonnais nés après 1900 (`"1900"^^xsd:gYear`).
  1. Afficher les noms et dates de naissance des lyonnais nés après 1900 avec, le cas échéant, leur date de décès.
  1. Afficher les noms de tous les lyonnais morts à Lyon.
  1. Afficher les noms de tous les lyonnais morts hors de France.
  1. Afficher toutes les villes françaises dont le maire est natif.
  1. Afficher tous les maires français (_i.e._ d'une ville de France) nés hors de France.
  1. Afficher tous les maires nés hors du pays où ils sont maires.
  1. Afficher le nombre de maires français nés hors de France.
  1. Afficher pour 10 villes françaises le nombre de natifs présents dans _DBPedia_.
  1. Afficher les 10 villes ayant le plus de natifs dans _DBPedia_.

Pour bien débuter, voici la réponse à la première requête. Vous pouvez copier-coller la requête dans le client _Yasgui_, et observer le résultat.

```sparql
PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX dbr: <http://dbpedia.org/resource/>
SELECT ?p 
WHERE {
  ?p a              dbo:Person;
     dbo:birthPlace dbr:Lyon.
}
```

---
## Requêtes originales sur une base _linked data_ (Compte-rendu)

*Remarque introductive* Le compte-rendu portera uniquement sur cette partie du TP. C'est un travail personnel, et donc le rendu est individuel. Vos CRs devront être déposés sur _Moodle_, en suivant les consignes énoncées ci-dessous.

**Enoncé** Choisissez une base de données _linked data_ (autre que _DBPedia_) et inventez deux requêtes sur cette base. 

*Consignes pour le rendu* :

- Rédigez un petit rapport (rapport de 3 pages maximum, au format Markdown de préférence, sinon Word ou pdf) comprenant, pour chacune des 2 requêtes, les détails suivants :

    - Préciser le _SparQl endpoint_ permettant d'accéder à la base que vous interrogez. Par exemple, pour la base des prix nobels, le _endpoint_ est http://data.nobelprize.org/sparql ; pour _DBpedia_, le _endpoint_ est http://dbpedia.org/sparql.
    - Le dessin RDF de la requête. Pour cela, vous pouvez utiliser [diagram.net](https://app.diagrams.net).
    - Le code _SparQL_ de la requête (que je puisse rejouer votre requête).
    - Les 3 ou 4 premiers résultats de la requête (copie d'écran).

N'oubliez pas d'inscrire votre nom sur le rapport, et de déposer un seul fichier compressé nommé _VotreNom_rendu1.zip_, sur Moodle, en respectant la deadline. Le site de dépôt de la plateforme est programmé pour ne plus accepter de compte-rendu au-delà de cette date.

Ce rapport sera évalué et comptera dans votre note finale. La note prendra en compte l'originalité des requêtes, et la qualité du code bien sûr !

Vous trouverez dans [ce lien](./Exemple_Rendu_TP1.zip) un exemple de rendu qui répond aux consignes.

### Bases _LoD_

Il existe des moteurs de recherche de bases, comme 

- [The Linked Open Data Cloud](https://lod-cloud.net/datasets), 
- [Linked open vocabularies](https://lov.linkeddata.es/dataset/lov/),
- [DataHub](https://old.datahub.io/), _from the Open Knowledge Fundation_.

Mais attention, beaucoup de bases sont inaccessibles (non mises à jour des adresses). Il faut donc en essayer plusieurs avant d'en trouver une valide !

Sinon, voici une [liste excel](https://docs.google.com/spreadsheets/d/15AXnxMgKyCvLPil_QeGC0DiXOP-Hu8Ln97fZ683ZQF0/edit#gid=54922684) contenant des adresses de nombreuses bases. Elle vous donne par exemple accès à la [BNF](https://data.bnf.fr/sparql/) (Bibliothèque National de France) dont voici une exemple de requête

```sparql
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX bio: <http://vocab.org/bio/0.1/>
SELECT ?auteur ?jour ?date1 ?date2 ?nom
WHERE {
?auteur foaf:birthday ?jour.
?auteur bio:birth ?date1.
?auteur bio:death ?date2.
OPTIONAL {?auteur foaf:name ?nom.}
}
ORDER BY (?jour) LIMIT 100
```


### Quelques bases _LoD_ particulières

Voici ci-dessous quelques bases que j'ai pu tester, mais vous êtes libres de choisir tout autre base si vous me précisez son _Sparql endpoint_ dans le rapport.


1. [Prix nobels](http://data.nobelprize.org/sparql).

La description de la structure des données se trouve en suivant [ce lien](https://data.nobelprize.org/specification/).

```sparql
PREFIX foaf: <http://xmlns.com/foaf/0.1/>

SELECT ?n1 ?n2 WHERE {
  ?p1 a         foaf:Person;
     foaf:name  ?n1.
} LIMIT 10
```

2. [_War Sampo_](https://ldf.fi/warsa/sparql).

     > _War sampo_ (la guerre de Sampo) s'est déroulée en Finlande durant la deuxième guerre mondiale.
     > Les textes dans cette base de données sont en suédois et finnois.

```sparql
PREFIX prisoners: <http://ldf.fi/schema/warsa/prisoners/>

SELECT ?causeDeath (count(?causeDeath) as ?count)
WHERE {
  ?p prisoners:cause_of_death ?causeDeath;
}
GROUP BY ?causeDeath
ORDER BY DESC(?count)
LIMIT 50
```

Ce [lien](https://www.ldf.fi/index.html) vous permet de consulter _linked Data Finland - Living Laboratory Data Service for the Semantic Web_, qui propose de nombreuses bases à interroger.


3. [WikiData](https://query.wikidata.org/sparql)

```sparql
PREFIX bd: <http://www.bigdata.com/rdf#> 
PREFIX wikibase: <http://wikiba.se/ontology#> 
PREFIX wd: <http://www.wikidata.org/entity/> 
PREFIX wdt: <http://www.wikidata.org/prop/direct/> 
select  ?object ?objectLabel
where {
  ?object wdt:P31 wd:Q6256.
  ?object wdt:P463 wd:Q458 

  SERVICE wikibase:label {
    bd:serviceParam wikibase:language "fr,en" .
  }
}
```

4. [European Patent Ontology](https://data.epo.org/linked-data/sparql.html)

La description de la structure des données se trouve en suivant [ce lien](https://data.epo.org/linked-data/documentation/patent-ontology-overview.html").

```sparql
prefix skos: <http://www.w3.org/2004/02/skos/core#>
prefix st3: <http://data.epo.org/linked-data/def/st3/>
prefix text: <http://jena.apache.org/text#>
prefix vcard: <http://www.w3.org/2006/vcard/ns#>
prefix xsd: <http://www.w3.org/2001/XMLSchema#>

SELECT ?application ?appNum ?filingDate ?authority {
  ?application rdf:type patent:Application ;
      patent:applicationNumber ?appNum ;
      patent:filingDate        ?filingDate ; 
      patent:applicationAuthority ?authority.
} LIMIT 10
```