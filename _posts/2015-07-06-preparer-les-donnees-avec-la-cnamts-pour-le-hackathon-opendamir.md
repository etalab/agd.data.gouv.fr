---
id: 121
title: Comment nous avons préparé le hackathon DAMIR
date: 2015-07-06T10:08:48+00:00
author: Alexis Eidelman
layout: post
guid: http://agd.data.gouv.fr/?p=121
permalink: /2015/07/06/preparer-les-donnees-avec-la-cnamts-pour-le-hackathon-opendamir/
image: /wp-content/uploads/2015/07/Hackathon-Damir2.jpg
categories:
  - Circulation des données
tags:
  - Billet technique
  - Evénement
---
L'objectif d'un hackathon est de montrer comment une mise é disposition de données permet de créer de nouveaux services et de réaliser de nouvelles études. Pour que les participants puissent réutiliser les données facilement et sans perdre de temps, quelques étapes préparatoires sont parfois nécessaires. D'autant plus lorsque ceéhackathon porte sur des données techniques, volumineuses et ayant un caractère personnel.

Illustrations de ces travaux préliminaires é partir de l'exemple du [hackathon é données de santé é](https://www.etalab.gouv.fr/retour-sur-le-premier-hackathon-donnees-de-sante "hackathon éédonnées de santééé") organisé par la _Caisse Nationale de l'Assurance Maladie des Travailleurs Salariés_ (CNAMTS) et Etalab en janvier dernier pour lequel l'équipe de l'Administrateur général des données (AGD) s'est mobilisée.

Avant toute chose, la première étape avant d'ouvrir des données consistait é éliminer les informations é caractère personnel de la base de données en vérifiant **l'impossibilité de réidentifier les individus (patients ou professionnels de santé)**.

L'équipe de la CNAMTS a adopté deux stratégies distinctes. Un [premier jeu de données](https://www.data.gouv.fr/fr/datasets/depenses-d-assurance-maladie-hors-prestations-hospitalieres-par-caisse-primaire-departement/) contient des données agrégées au niveau du département avec un nombre limité de variables alors qu'un second jeu de données, l'[OpenDAMIR](https://www.data.gouv.fr/fr/datasets/open-damir-base-complete-sur-les-depenses-dassurance-maladie-inter-regimes/), contient l'ensemble des variables contenues dans le jeu de données initial mais agrégées par groupe de régions.

Une fois les risques de réidentification écartés, nous avons **standardisé la base de données pour en faciliter la réutilisation.** En effet, les données fournies par la CNAMTS étaient issues duésystème d'information interne et pensées pour seséusages. Pour faciliter la réutilisation des données par un public plus large, nous avonsé:

  1. remplacé les longs libellés de certaines variables par des codes et créer une table de passage entre les libellés et les code;
  2. supprimé les variables géographique redondantes en ne conservant que le niveau géographique le plus détaillé;
  3. écrit des scripts R et Python permettant de travailler facilement sur des niveaux géographiques agrégés.

Ces opérations ont permis de réduire par quatre la taille de la base sur le disque et de faciliter le chargement des données sur un ordinateur. Le volume de données (près de 200 GO et un milliard et demi de lignes) restait cependant important. Pour permettre aux participants d'accéder aux données le jour J nous avons mis un place une base de données PostgreSQL sur un serveur et installé un réseau Ethernet local. Cela a permis aux participants de faire plus d'un million de requètes et de télécharger 650 Go de données au total dans de bonnes conditions. Nous avions également préparé des programmes R et python pour faciliter l'accès é la base PostresSQL.

Enfin, le succès d'un hackathon repose sur **l'exploitation des données** et les réutilisations qui en résultent. Or, avoir accès aux données et en connaétre le format ne suffit pas pour les utiliser ces données, il est aussi nécessaire d'en comprendre leur contenu. C'est pour cette raison que nous nous sommes associés avec l'équipe de la CNAMTS **pour élaborer un [wiki](https://github.com/SGMAP-AGD/DAMIR/wiki/remboursement) é destination des utilisateurs.**

Le DAMIR étant une base administrative, il était important de préciser la nature des informations qu'elle contient et les concepts qui leurs sont associés. On trouve par exemple sur ce wiki une vision synthétique de ce qu'est un acte médical mais aussi une description technique des tables et un dictionnaire des codes. La marche é suivre pour se connecter au serveur avec des exemples de codes sont aussi disponible sur le wiki. Ce dernier a été précieux lors du hackathon puisqu'il a permis aux participants d'ètre presque autonomes sur l'utilisation des données.

C'est en général en croisant différentes bases de données qu'on obtient les résultats les plus intéressants. Pour faciliter le travail des participants, nous avons aussi préparé des données en open data susceptibles d'ètre croisées avec la base du DAMIR. Nous avions ainsi préparé les données de démographie médicale issue du [Répertoire partagé des professions de santé](https://www.data.gouv.fr/fr/datasets/la-demographie-des-medecins-rpps/), mes données sur la [structure démographique par département](http://www.insee.fr/fr/themes/detail.asp?reg_id=99&ref_id=estim-pop) produites par l'Insee, les [données sur la météo](https://github.com/SGMAP-AGD/DAMIR/tree/master/fichiers_supplementaires/meteo), les [données d'accidentologie](https://www.data.gouv.fr/fr/datasets/base-de-donnees-accidents-corporels-de-la-circulation-sur-6-annees/) ou encore les [limites administratives des départements](https://www.data.gouv.fr/fr/datasets/limites-administratives-francaises-issues-d-openstreetmap/) pour pouvoir réaliser des cartes.

Le jour du hackathon, nous avons aussi participé activement en proposant des sujets et en prenant part aux différents groupes. Les codes et réutilisations peuvent ètre trouvés sur [data.gouv.fr](https://www.data.gouv.fr/fr/datasets/open-damir-base-complete-sur-les-depenses-dassurance-maladie-inter-regimes/).
