
# TP _Big Data_, ECC

Cet espace recueille les fichiers de cours et TP du module _Technologies Informatique du Big Data_, enseigné à l'École Centrale de Casablanca. Tous les rendus de TP se feront sur le [site edunao](https://centrale-casablanca.edunao.com/course/view.php?id=179). Le rendu de la fiche de synthèse se fera directement sur l'espace git (détails ci-dessous).

[_Stéphane Derrode_](mailto:stephane.derrode@ec-lyon.fr), École Centrale de Lyon, Dpt MI, LIRIS (CNRS UMR 5205).



## Informations générales

> - 6 séances de 4h, réparties en 2 phases (12-14 décembre 2022 et 16-18 janvier 2023).
> - Slides des cours:
     >
     > - [Introduction : Big Data, données personnelles et éthique des données](Slides/Pres_IntroBigData.pdf)
     > - [Open Data](Slides/Pres_OpenData.pdf)
     > - [Linked Open Data](Slides/Pres_LOD.pdf)
     > - [Hadoop](Slides/Pres_Hadoop.pdf)
     > - [Spark](Slides/Pres_Spark.pdf)

> - Des compte-rendus de TPs à rendre.
> - Une Fiche de Synthèse (FS) à rédiger sur un sujet associé au big data. Les consignes sont disponibles dans [ce répertoire](./Template_FS/README.md) et seront présentées lors de la première séance.



## Déroulé des séances


### Séance #1 (12.12.2022) - Introduction au _Big Data_ et à l'_Open Data_

- **Objectif du cours**

    > - Présentation des objectifs du module.
    > - Introduction au _Big Data_: enjeux éthiques, économiques & scientifiques.
    > - Présentation de la Fiche de Synthèse (FS), à rédiger par groupe de 4 à 5 étudiants. Celle-ci doit être préparée tout au long du module, la date de remise est fixée à la date de la dernière séance de cours. Les consignes pour la rédaction (utilisation de _Markdown_ et de _git_) et le rendu sont détaillées dans le répertoire [Template_FS](./Template_FS/README.md).
    > - [Question Wooclap](https://app.wooclap.com/FETQLU)
    > - Apprentissage de _git_, avec l'outil _GitHub Desktop_ et directement en ligne de commandes (avec un _Terminal_). Le scénario du tutoriel présenté en séance est disponible dans le [dossier git](./tuto-git-gitlab).
    > - Introduction à l'_Open Data_. Vidéos utilisées en cours:
        > 
        > - [L'open data à la loupe](https://www.youtube.com/watch?v=6WtviEVPkJI).
        > - [_How we found the worst place to park in New York City_](https://www.ted.com/talks/ben_wellington_how_we_found_the_worst_place_to_park_in_new_york_city_using_big_data).
  
- **Vidéos complémentaires**

    > - [Le Big Data pour mieux nous comprendre](https://www.ted.com/talkkenneth_cukier_big_data_is_better_data?language=fr).
    > - [_Let's pool our medical data_](https://www.ted.com/talks/john_wilbanks_let_s_pool_our_medical_data).
    > - [_Why privacy matters?_](https://www.ted.com/talks/glenn_greenwald_why_privacy_matters#t-46573).
    > - [_Big Data will impact every part of your life_](https://www.youtube.com/watch?v=0Q3sRSUYmys).
    > - [_Big data and dangerous ideas_](https://www.youtube.com/watch?v=tLQoncvCKxs).
    > - [_Big Data and the Rise of Augmented Intelligence_](https://www.youtube.com/watch?v=mKZCa_ejbfg). 
    > - [_How Big Data Can Influence Decisions That Actually Matter_](https://www.youtube.com/watch?v=C6WKt6fJiso). 
    > - [_Is Big Data Killing Creativity?_](https://www.youtube.com/watch?v=A1XibEzp6K0). 
    > - [_Analyzing and modeling complex and big data_](https://www.youtube.com/watch?v=8DqQCZMawNg).  
    > - [_How to Monetize Big Data_](https://www.youtube.com/watch?v=8DqQCZMawNg). 
    > - [_How to predict the future with big data_](https://www.youtube.com/watch?v=J0bp2kUh9hw).
    > - [_Demand on a more open-source government_](https://www.ted.com/talks/beth_noveck_demand_a_more_open_source_government#t-66622).
    > - [L'Open Data, Avenir des Big Data](https://www.youtube.com/watch?v=MUI6Rwn4Qq0).
    > - [_Linked Open Data - What is it?_](https://www.youtube.com/watch?v=uju4wT9uBIA).  
   

### Séance #2 (13.12.2022) - _Linked Open Data_ et TP _SparQL_

- **Objectif du cours**

    > - [Question Wooclap](https://app.wooclap.com/MIZTRT)
    > - Introduction aux données liées (_Linked Data_ ou _Linked Open Data_).
    > - Liens vers des vidéos vues en cours :
        >
        > - [Tim Berners-Lee : _The next Web_](https://www.ted.com/talks/tim_berners_lee_the_next_web).
        > - [_What is Linked Data? Manu Sporny_](https://www.youtube.com/watch?v=4x_xzT5eF5Q).
    >
    > - Travail sur le [TP1](./TP1) avec _SparQL_. La fin de l'énoncé fait l'objet d'un compte-rendu individuel.


### Séance #3 (14.12.2022) - _Framework Hadoop map-reduce_

- **Objectif du cours**

    > - Présentation du _framework Hadoop_/_map-reduce_
    > - Fiche de Synthèse
        >
        > - Formez les groupes, déposez les noms et les adresses mail et les sujets de votre FS sur le fichier [hébergé ici](https://partage.liris.cnrs.fr/index.php/s/FegdnkcY7xSgAr2).    
        > - Après avoir créé un compte sur la plateforme [GitLab](https://gitlab.com/users/sign_in) ou [GitHub](https://github.com/), créez un projet privé pour la FS (me désigner `reporter` de chaque FS, mon pseudo _GitLab_ ou _GitHub_: _stephane.derrode@ec-lyon.fr_), selon les modalités exposées dans le dossier [Template_FS](./Template_FS/README.md). Cela me permettra de voir l'avancée de vos travaux (espionnage !). 
    
    > - Présentation du [TP #2](./TP2) qui se déroulera durant la seconde phase (en janvier). En préparation à ce TP, installez _Docker_ et le container _Docker Linux/Hadoop_ selon les consignes données dans **la PARTIE 2** du TP #2. Attention, le téléchargement est très volumineux et nécessite une machine avec au moins 3 GO libre de disque dur! Prenez-vous en avance pour faire cette installation!


---

### Séance #4 (16.01.2023) - TP _Hadoop map-reduce_

- **Objectif du cours**

    > - Rappel sur Hadoop _map-reduce_
    > - [Question Wooclap](https://app.wooclap.com/RUMGPO)
    > - Présentation du [TP #2](./TP2). La fin de l'énoncé fait l'objet d'un compte-rendu individuel ou en binôme.

### Séance #5 (17.01.2023) - Framework _Spark_

- **Objectif du cours**

    > - Présentation du framework _Spark_.

### Séance #6 (18.01.2023) - TP _Spark_

- **Objectif du cours**

    > - Commencez le [TP #3](./TP3), depuis la section `Tester les scripts vus en cours`. La fin de l'énoncé fait l'objet d'un compte-rendu individuel ou en binôme.
    > - La partie 4 de ce TP (portant sur _Spark streaming_) est optionnelle.
