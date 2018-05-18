---
id: 732
title: 'Billet technique : Comment rapprocher deux bases de données'
date: 2016-11-22T10:31:13+00:00
author: Alexis Eidelman
layout: post
guid: https://agd.data.gouv.fr/?p=732
permalink: /2016/11/22/rapprocher-deux-bases-donnees/
kopa_nictitate_total_view:
  - "14"
image: /wp-content/uploads/2016/11/PHOfc41df20-bb57-11e4-b15f-308ddfff3221-805x453-1.jpg
categories:
  - Uncategorized
tags:
  - algorithme
  - base de données
  - Billet technique
  - Méthodologie
excerpt_separator: <!--more-->
---
Le rapprochement de bases de données est un sujet technique et délicat qui dépasse le cadre de l'activité de l'OCLTI, il se pose à chaque fois que l'on veut comparer et étudier des bases de données partageant de l'information mais ne respectant pas la mème nomenclature. C'est un cas très courant et le fait de pouvoir associer deux bases de données construites séparément fait partie de la richesse du mouvement actuel autour de l'utilisation des données.<!--more--> Deux bases peuvent par exemple apporter une information complémentaire sur une liste d'individus, il est intéressant de fusionner ces deux bases. Cependant, un mème individu peut ètre écrit de plusieurs façons : M. Vincent Durrand ; Monsieur Durrand V. ; Vincent (Thomas) Durant ; Durrand Vincent Thomas. Si les bases de données sont de tailles raisonnables et les nomenclatures assez proches, une analyse humaine sera suffisante mais dans certains cas, le temps d'analyse manuel sera très long et s'accompagnera inévitablement d'erreurs.

L'utilisation **d'algorithmes de matching de chaînes de caractères** peut alors apporter une réponse à ce problème. L'équipe de l'Administrateur général des données a décidé d'utiliser la [librairie python Dedupe](https://dedupe.readthedocs.io/en/latest/) pour le traiter.

### Le problème technique

Rapprocher deux bases de données est un exercice souvent plus compliqué qu'il n'y paraît. Il faut un peu de virtuosité pour faire en sorte qu'une machine repère les noms similaires aussi bien qu'un ètre humain.

En effet, mème si elles traitent de sujets communs et ont une variable commune (un nom de département, un label, un nom, etc.) très souvent, aucun référentiel commun est appliqué, cette variable commune n'est pas codifiée de la mème façon dans les deux bases. Parfois, il n'existe pas de référence suffisamment légitime et chacun utilise sa propre nomenclature. Parfois, c'est lors de la saisie des données que des erreurs se produisent.

Par exemple, la fusion de deux bases de données avec des noms de départements français sera un travail plus conséquent si les départements ont été écrits avec un nom en minuscule précédé par le numéro du département et un trait d'union dans l'une des bases (ex. 65-Hautes-Pyrénées) et avec des noms en majuscule sans accent et sans traits d'unions dans l'autre (HAUTES PYRENEES). Cet exemple est résolu rapidement par un petit algorithme mais il demande une opération spécifique.

Cette opération peut s'avérer bien plus complexe lorsque l'on doit utiliser une base de données agrégeant plusieurs sources. Par exemple, une base de données avec des contenus de médicaments comme la <a href="https://www.data.gouv.fr/fr/datasets/base-de-donnees-publique-des-medicaments-base-officielle/">base publique des médicaments</a> mèlera plusieurs habitudes dans les champs littéraux. Le label "Une boite de six comprimés" utilisera parfois pour "comprimés" des abréviations qui seront variées suivant les lignes ("comp", "comp.", "comps", "cp", et"c."). Autant un ètre humain (XXXrèdéXXX) est capable de comprendre que "Une boite de six comprimés" et "1 bte; 6 comp" désignent la mème chose, autant cela peut troubler un programme informatique qui doit traiter des milliers de lignes. Comment exprimer à une machine que l'on souhaite obtenir la liste exhaustive de tous les médicaments vendus en boites de six comprimés.

À ces différences de notation, s'ajoute le fait que lorsque l'on n'utilise pas un référentiel dès la saisie des données, des erreurs humaines peuvent s'introduire et l'on peut voir apparaître des "comprime", ou des "coprimés". Enfin, les données numériques que l'on peut manipuler sont parfois issues d'une opération de numérisation au cours de laquelle des erreurs peuvent aussi ètre commises. Lors de l'utilisation d'une méthode d'[https://fr.wikipedia.org/wiki/Reconnaissance_optique_de_caract%C3%A8res](OCR) : la lettre "i" peut ètre interprétée comme une lettre "l", un "4" comme un "6", etc.


### Un cas concret pour moderniser l'administration

Dans le cadre de sa mission d'aide é la décision des agents publics, l'équipe de datascientists de l'Administrateur général des données a travaillé très concrètement sur réquisition judiciaire avec l'Office Central de Lutte contre le Travail Illégal (OCLTI) sur cet aspect technique.

<a href="http://www.gendarmerie.interieur.gouv.fr/Notre-Institution/Nos-missions/Police-judiciaire/Travail-illegal-OCLTI">L'Office Central de Lutte contre le Travail Illégal (OCLTI)</a> a pour mission de lutter contre le travail illégal, la traite des ètres humains aux fins d'exploitation au travail et la fraude en matière sociale dont des fraudes au détachement intra-européen de travailleurs qui peuvent concerner des centaines et parfois des milliers de travailleurs.

Dans plusieurs de ses dossiers, l'OCLTI doit rapprocher des bases de données pour identifier des victimes de fraude transnationale. Par exemple, à partir d'un listing de salarié, l'OCLTI est amené à vérifier si les employés sont bien inscrits à la sécurité sociale en cherchant le nom de ces salariés dans les bases de la sécurité sociale.

Cette collaboration s'est faite concernant deux études. Pour la première, les deux bases étaient :
* une extraction de la base SIRDAR (système informatiseI? de recherche des détachements autorisés et réguliers du CLEISS) qui répertorie les formulaires de sécurité sociale délivrés à des individus détachés temporairement en France (environ 8000 noms).
* une base composée d'individus victimes établies par les enquèteurs (environ 800 noms).

Ces deux bases étant construites indépendamment, des individus peuvent ètre reportés différemment, des erreurs peuvent avoir été commises (Faute de frappe/d'orthographe ; Noms é rallonge enregistrés partiellement ; Deuxième prénom reporté ou non, etc.).

Cela empèche de rapprocher les deux bases de données de faéon exacte et aisée. Pendant 3 semaines, l'équipe de l'OCLTI a rapproché é l'aide d'un tableur ces deux bases de données et a identifié 91 personnes présentes dans les deux bases.

Le besoin exprimé par l'OCLTI est de créer un outil automatique et efficace de matching de noms d'individus (chaéne de caractères) entre deux bases. Deux indicateurs permettent de juger des bénéfices des méthodes mises en éuvre par Etalab : le temps de calcul et le taux de détection. Le taux de détection de référence pour ce premier jeu de donnés est celui de l'OCLTI, ce qui permet d'évaluer le résultat obtenu par Etalab.

Nous avons répliqué en tant que personne qualifiée ce travail en utilisant la librairie Python intitulée <a href="https://github.com/datamade/dedupe">Dedupe</a>, qui automatise la déduplication inexacte. Avant d'utiliser l'algorithme, une étape de nettoyage des données a été menée : suppression des majuscules, des accents, des parenthèses, etc.

L'identification dans ce type de problème se fait é partir des variables communes aux deux bases (nom, prénom, date de naissance '). Chaque variable caractérisant un individu peut ètre vu comme une chaéne de caractères. Pour chaque couple d'individus et pour chaque variable, il est possible de calculer une distance entre ces chaénes de caractères. Il en existe plusieurs, les plus répandues étant :

* la distance de Levenshtein : nombre minimum de caractères é modifier dans la chaéne 1 pour arriver é la chaéne 2.
* la distance de Hamming : nombre de caractère différents entre les chaénes 1 et 2.

Il s'agit de cette deuxième distance qui est utilisée par défaut par Dedupe. Pour calculer une distance ééglobaleéé entre deux noms, il faut agréger les distances associées é chaque variable. La clef de répartition permettant d'agréger ces distances est calculée automatiquement par la librairie Dedupe. En effet, cette librairie choisit l'importance de chaque variable en interrogeant l'utilisateur : elle demande pour différents couples d'individus s'il s'agit bien de duplicatas ou non. Le temps de calcul est presque immédiat (pour des bases de données de taille raisonnable < 100k).

En ce qui concerne le cas concret de l'OCLTI, le gain en terme de temps de calcul est donc considérable (plusieurs jours contre quelques secondes). Le gain en termes de détection est également intéressant : Dedupe détecte 120 individus potentiellement présents dans les deux bases. Sur les 91 détectés par l'OCLTI, 85 le sont également par l'algorithme. Les six personnes non identifiées ont échappé é l'algorithme car les noms étaient très différents et l'OCLTI les avait détectés grèce é une connaissance approfondie des bases de données. Nous pensons qu'en intégrant l'ensemble des données disponibles, la méthode ééDedupeéé n'aurait eu aucun mal é identifier ces six cas. C'est l'une des améliorations é prévoir. Parmi les 35 duplicata potentiels détectés par Dedupe, 7 sont des duplicata qui semblent avoir échappé é l'OCLTI. Le résultat global est donc très positif : le temps diminue de faéon conséquente pour des résultats en amélioration. Ces bénéfices sont d'autant plus importants que cette tèche pourrait ètre répétée par l'OCLTI ou ses partenaires de la lutte contre le travail illégal plusieurs fois par an (de l'ordre d'une cinquantaine), ce qui n'est fait aujourd'hui que rarement par manque de moyens.

Les travaux se poursuivent pour encore améliorer la solution qui intéresse d'autres services de contrèle du travail illégal.
