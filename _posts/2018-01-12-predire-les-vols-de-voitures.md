---
id: 946
title: Prédire les vols de voitures ?
date: 2018-01-12T12:59:45+00:00
author: Florian Gauthier
layout: post
guid: /?p=946
permalink: /2018/01/12/predire-les-vols-de-voitures/
categories:
  - Science des données
image: /wp-content/uploads/2017/10/6-Predvol-predictions-quotidiennes.png
excerpt: En 2015, l'équipe de l'Administrateur général des données au sein de la DINSIC a développé en collaboration avec le Service des technologies et des systèmes d'information de la Sécurité intérieure (ST(SI)è), un modèle de prédiction des vols liés aux véhicules. Cette collaboration a permis de développer **Predvol**, un outil d'aide à la décision pour les policiers et les gendarmes, comprenant une prédiction quotidienne du risque de vols, une carte de l'historique des vols et une typologie des quartiers en fonction de la nature des infractions qui y sont commises.
---
**Résumé :**

En 2015, l'équipe de l'Administrateur général des données au sein de la DINSIC a développé en collaboration avec le Service des technologies et des systèmes d'information de la Sécurité intérieure (ST(SI)è), un modèle de prédiction des vols liés aux véhicules. Cette collaboration a permis de développer **Predvol**, un outil d'aide à la décision pour les policiers et les gendarmes, comprenant une prédiction quotidienne du risque de vols, une carte de l'historique des vols et une typologie des quartiers en fonction de la nature des infractions qui y sont commises.

<p class="p3">
  <span class="s1">Ce projet, qui fut l'un des premiers de l'AGD, vit le jour lors d'une rencontre entre Etalab et le ST(SI)è. Les responsables du ST(SI)è, soucieux de tirer parti des avancées en matière de data-sciences, cherchaient un appui scientifique pour expérimenter des techniques d'apprentissage automatique (<i>machine learning</i>) sur un territoire. Le département de l'Oise, particulièrement exposé aux vols de voitures, réunissait les conditions pour lancer un projet.</span>
</p>

[<img class="wp-image-952 aligncenter" src="/wp-content/uploads/2017/10/1-oise_2015.jpeg" alt="" srcset="/wp-content/uploads/2017/10/1-oise_2015.jpeg 2020w, /wp-content/uploads/2017/10/1-oise_2015-300x216.jpeg 300w, /wp-content/uploads/2017/10/1-oise_2015-768x554.jpeg 768w, /wp-content/uploads/2017/10/1-oise_2015-1024x738.jpeg 1024w" sizes="(max-width: 643px) 100vw, 643px" />](/wp-content/uploads/2017/10/1-oise_2015.jpeg)

<p class="p6" style="text-align: center;">
  <span class="s1"><i>Vols de véhicules dans l'Oise en 2015 (Source : Datafrance)</i></span>
</p>

&nbsp;

<p class="p3">
  <span class="s1">Définir une problématique claire est indispensable au démarrage d'un projet de data-sciences. S'agissant des vols de voitures, nous sommes partis du constat suivant :</span>
</p>

[<img class="wp-image-951 aligncenter" src="/wp-content/uploads/2017/10/2-patrouilles.jpeg" alt=""  />](/wp-content/uploads/2017/10/2-patrouilles.jpeg)

<p class="p6" style="text-align: center;">
  <span class="s1"><i>Patrouilles vs Répartition des vols (2014)</i></span>
</p>

&nbsp;

<p class="p3">
  <span class="s2">Un simple coup d'œil permet de s'apercevoir que certaines zones très surveillées par les forces de l'ordre, observent aussi de nombreux vols de véhicules (zones A), tandis que d'autres, bien que très touchées par les vols de véhicules, sont très peu empruntées par les patrouilles (zones B).</span>
</p>

<p class="p6">
  <span class="s1"><i>Dans quelle mesure serait-il possible d'anticiper les vols de voitures afin d'aboutir à une meilleure orientation des patrouilles de police et de gendarme ?</i></span>
</p>

<p class="p3">
  <span class="s1">Afin de répondre à cette problématique, le ST(SI)è nous a transmis des données provenant directement des bases de dépèts de plaintes auprès de la police et de la gendarmerie : LRPPN et LRPGN. En tout, 3 ans d'historique de vols liés aux véhicules en ont été extraits. Chaque ligne correspondait à une infraction définie par un lieu (coordonnées XY), une date ainsi que quelques informations &#8211; souvent manquantes &#8211; sur le véhicule volé.</span>
</p>

<p class="p3">
  <span class="s1">Par ailleurs, <b>un contact régulier avec les utilisateurs finaux</b> s'est très vite imposé afin d'identifier précisément les problématiques des acteurs de terrain et leurs façons de travailler. Deux besoins très distincts ont tout de suite fait surface :</span>
</p>

<p class="p3">
  <span class="s1">1) Cibler les zones les plus à risques en amont de la patrouille</span>
</p>

<p class="p3">
  <span class="s1">2) Un outil d'aide à la décision pendant la patrouille</span>
</p>

<p class="p3">
  <span class="s1">Sur ce premier point, il convenait tout d'abord de définir un découpage géographique optimal afin d'<i>entraîner</i> nos algorithmes. Le découpage IRIS proposé par l'INSEE, apportant le meilleur arbitrage taille/quantité de données disponibles, s'imposa comme le meilleur candidat. Ce dernier permit en effet d'enrichir notre base de données d'apprentissage avec </span><span class="s1"><b>plus de 600 variables socio-démographiques sur ces zones </b>(taux de chèmage, scolarisation des jeunes, nombre de commerces à proximité, èges moyens, '). Ajouté à cela, nous avons calculé d'autres indicateurs sur les circonstances temporelles des vols : Y-avait-il eu un vol la veille ? L'avant-veille ? Dans les quartier voisins ? Quelle était la météo du jour ? '</span>
</p>

<p class="p3">
  <span class="s1">Le principe est en effet d'amener, <b>sans a priori</b>, le maximum de variables dans notre base de données (ici plus de 650 variables) puis de laisser les algorithmes de machine learning sélectionner les meilleures prédicteurs pour anticiper les vols de voitures.</span>
</p>

<p class="p3">
  <span class="s1">Nous avons alors testé 3 grandes familles d'algorithmes afin d'anticiper au mieux, chaque jour, les vols liés au véhicules dans les 799 quartiers l'Oise :</span>
</p>

<p class="p3">
  <span class="s1">A) Des algorithmes basés sur une grande quantité de variables</span>
</p>

<p class="p3">
  <span class="s1">Ces algorithmes figurent parmi les plus classiques de la littérature en matière de machine learning : régression logistique, forèts aléatoires, boosting, forèts aléatoires extrèmement randomisées, XGBoost' Ces algorithmes utilisent une très grande quantité de variables, sélectionnent les meilleurs prédicteurs en leur associant des pondérations et les utilisent pour tenter anticiper la variable d'intérèt.</span>
</p>

<p class="p3">
  <span class="s1">B) Les algorithmes de PredPol, une entreprise américaine connue dans ce domaine </span>
</p>

<p class="p3">
  <span class="s1">Revendiquant la place numéro 1 en matière de <i>predictive policing</i>, la société PredPol utilise des algorithmes initialement développés par un sismologue français, David Marsan, afin de prédire les répliques des séismes. PredPol a fait l'hypothèse que <b>les crimes se comportent comme les séismes</b> :</span>
</p>

<p class="p3">
  <span class="s1">&#8211; <b>il existe un risque-terrain </b>: des zones plus sujettes au crime (calculé en fonction du passé)</span>
</p>

<p class="p3">
  <span class="s1">&#8211; <b>les crimes entraînent des répliques (on parle d'effet de "contagion")</b> c'est-é-dire que lorsqu'il y a un crime dans une zone, la probabilité qu'il en survienne un autre dans une zone géographique proche est plus grande et décroét avec le temps.</span>
</p>

<p class="p3">
  <span class="s1">Nous avons implémenté leurs algorithmes et les avons testé sur les vols liés aux véhicules. Voici les résultats :</span>
</p>

[<img class=" wp-image-950 aligncenter" src="/wp-content/uploads/2017/10/3-contagion.png" alt="" srcset="/wp-content/uploads/2017/10/3-contagion.png 558w, /wp-content/uploads/2017/10/3-contagion-300x204.png 300w" sizes="(max-width: 443px) 100vw, 443px" />](/wp-content/uploads/2017/10/3-contagion.png)

<p class="p6" style="text-align: center;">
  <i>Nombre de répliques</i>
</p>

<p class="p3">
  <span class="s1">Deux constats :</span>
</p>

<ul class="ul1">
  <li class="li3">
    <span class="s1">Les vols de véhicules dans l'Oise </span><span class="s3">n'ont pas de mémoire (Tetha'0).</span>
  </li>
  <li class="li3">
    <span class="s1">Seuls le "risque terrain"du quartier est important.</span>
  </li>
</ul>

<p class="p3">
  <span class="s1">Ce deuxième constat nous a alors conduit à tester notre troisième algorithme.</span>
</p>

<p class="p3">
  <span class="s1">C) Les cartes de chaleurs évolutives</span>
</p>

<p class="p3">
  <span class="s1">Une carte de chaleur est finalement exactement comme le modèle de PredPol sauf qu'on enlève la complexité du facteur de contagion. On prédira comme zone la plus risquée demain, la zone dans laquelle ont été observés le plus de vols dans le passé. Il convient désormais de définir ce fameux "passé". En effet, la technique des "punaises sur la carte" (infractions du dernier mois) est toujours couramment utilisée par la police et la gendarmerie. Notre idée ici était de <b>trouver l'historique optimal </b><strong>qu'il faut utiliser afin d'obtenir la carte de chaleur prédictive la plus pertinente.</strong></span>
</p>

&nbsp;

[<img class=" wp-image-949 aligncenter" src="/wp-content/uploads/2017/10/4-historique-optimal.png" alt="" srcset="/wp-content/uploads/2017/10/4-historique-optimal.png 892w, /wp-content/uploads/2017/10/4-historique-optimal-300x165.png 300w, /wp-content/uploads/2017/10/4-historique-optimal-768x423.png 768w" sizes="(max-width: 828px) 100vw, 828px" />](/wp-content/uploads/2017/10/4-historique-optimal.png)

<p style="text-align: center;">
  <em>Capacité prédictive et précision du HotSpot en fonction de l'historique utilisé (train_size)</em>
</p>

&nbsp;

<p class="p3">
  <span class="s1">Nous avons comparé les différents historiques utilisés selon les deux facteurs clés d'un modèle prédictif : la capacité prédictive et la précision du modèle. Un historique trop petit (les fameuses punaises) pénalisent grandement la capacité prédictive du modèle, tandis qu'un historique trop grand pénalise sa précision. Afin d'obtenir le meilleur ratio capacité prédictive / précision, <b>construire notre carte de chaleur sur neuf mois semblait le seuil optimal.</b></span>
</p>

<p class="p3">
  <span class="s1">Une fois nos modèles construits, il s'agissait ensuite de les comparer. La méthodologie est très classique : les algorithmes ont été entraénés sur une partie de la base de données (la première année d'infractions) puis testés sur une seconde partie que les algorithmes n'avaient jamais vu (les deux dernières années). Les résultats furent sans appel :</span>
</p>

[<img class=" wp-image-948 aligncenter" src="/wp-content/uploads/2017/10/5-comparaison-modeles-e1509370478313.png" alt="" srcset="/wp-content/uploads/2017/10/5-comparaison-modeles-e1509370478313.png 881w, /wp-content/uploads/2017/10/5-comparaison-modeles-e1509370478313-300x183.png 300w, /wp-content/uploads/2017/10/5-comparaison-modeles-e1509370478313-768x468.png 768w" sizes="(max-width: 669px) 100vw, 669px" />](/wp-content/uploads/2017/10/5-comparaison-modeles-e1509370478313.png)

<p style="text-align: center;">
  <em>Pourcentage de vols couverts (moyenne sur les 6 mois du test) en fonction du nombre d'IRIS couverts chaque jour</em>
</p>

&nbsp;

<p class="p3">
  <span class="s1">Les modèles prédictifs donnaient tous d'excellents résultats : <b>cibler en moyenne 10 % des quartiers prédits les plus risqués par le modèle permettait de couvrir 50% des vols.</b></span>
</p>

<p class="p3">
  <span class="s1">De plus, <b>le modèle le plus simple </b>(carte de chaleur prédictive)<b> permettait d'obtenir des résultats quasiment identiques aux modèles les plus complexes </b>(celui de PredPol, notamment)</span>
</p>

<p class="p3">
  <span class="s1"><i>Simple is Beautiful. </i>Cet adage bien connu prit alors tout son sens. Pourquoi ajouter un coût en complexité important lorsqu'on peut faire <i>presque </i>aussi bien avec un modèle simplissime ? Cela est d'autant plus vrai dès lors qu'on envisage d'intégrer nos travaux lors de la mise en production dans les systèmes d'information de l'état dont les environnements ne sont pas toujours prèts é recevoir des calculs complexes.</span>
</p>

<p class="p3">
  <span class="s1">Le modèle choisi, nous avons construit un outil baptisé "PredVol", optimisé pour un usage en mobilité (sur tablette) afin de rendre disponibles les résultats des prédictions journalières aux opérationnels de terrain. Nous avons doté PredVol de 3 onglets, l'un permettant de visualiser les quartiers prédits les plus risqués par le modèle, le second affichant une typologie des quartiers en fonctions des types de vols les plus présents dans chaque quartier, et un troisième permettant de visualiser les faits passés sur une carte.</span>
</p>

<p class="p3">
  <span class="s1">Côté Gendarmerie, l'outil a été intégré aux outils décisionnels et testé au sein de la compagnie de Compiègne à partir de mai 2016. Côté Police nationale, l'outil a été testé par les agents de la Direction départementale de la sécurité publique (DDSP) de Beauvais et notamment en patrouille par la brigade anti-criminalité (BAC).</span>
</p>

[<img class="alignnone size-full wp-image-947" src="/wp-content/uploads/2017/10/6-Predvol-predictions-quotidiennes.png" alt="" srcset="/wp-content/uploads/2017/10/6-Predvol-predictions-quotidiennes.png 1600w, /wp-content/uploads/2017/10/6-Predvol-predictions-quotidiennes-300x165.png 300w, /wp-content/uploads/2017/10/6-Predvol-predictions-quotidiennes-768x421.png 768w, /wp-content/uploads/2017/10/6-Predvol-predictions-quotidiennes-1024x562.png 1024w" sizes="(max-width: 1600px) 100vw, 1600px" />](/wp-content/uploads/2017/10/6-Predvol-predictions-quotidiennes.png)

<p class="p7" style="text-align: center;">
  <span class="s1"><i>PredVol &#8211; Prédictions quotidiennes</i></span>
</p>

<p class="p3">
  <span class="s1">Pendant 6 mois d'expérimentation, nous avons eu l'occasion d'améliorer l'outil PredVol afin qu'il réponde au mieux aux usages opérationnels. Cette étape cruciale nous a par exemple permis, en patrouillant avec la BAC de Beauvais, de réaliser que les boutons de sélection étaient trop petits pour ètre utilisés dans les virages.é</span><span class="s1">Après 6 mois d'expérimentation, nous avons réalisé que l'essentiel de l'attention des patrouilles se dirigeait non pas sur les prédictions quotidiennes, mais sur la simple visualisation des faits passés. En effet,<b> </b>si<b> les prédictions &#8211; bien que toujours très performantes &#8211; ne permettaient que de confirmer les zones é risques connues par les opérationnels</b>,<b> </b> la simple visualisation des faits (onglet 3) représentait un très net progrès dans leur usage quotidien.</span>
</p>

Fort de ce constat, nous avons développé un nouvel outil sur-mesure pour les brigades et cette fois entièrement porté sur la visualisation des infractions :

[<img class="alignnone size-full wp-image-993" src="/wp-content/uploads/2018/01/MapVHL-copie.jpg" alt="" srcset="/wp-content/uploads/2018/01/MapVHL-copie.jpg 3346w, /wp-content/uploads/2018/01/MapVHL-copie-300x150.jpg 300w, /wp-content/uploads/2018/01/MapVHL-copie-768x383.jpg 768w, /wp-content/uploads/2018/01/MapVHL-copie-1024x510.jpg 1024w, /wp-content/uploads/2018/01/MapVHL-copie-239x118.jpg 239w" sizes="(max-width: 3346px) 100vw, 3346px" />](/wp-content/uploads/2018/01/MapVHL-copie.jpg)

<p class="p7" style="text-align: center;">
  <span class="s1"><i>MapVHL &#8211; Visualisation des infractions</i></span>
</p>

<p class="p3">
  Ainsi qu'un autre permettant de visualiser <strong>les découvertes de véhicules volés</strong>, permettant ainsi aux brigades d'orienter leurs recherches lorsqu'un véhicule est volé, en fonction de sa marque et de son modèle.
</p>

<p class="p6" style="text-align: left;">
  <span class="s1">Enfin, permettre aux agents du terrain de visualiser les faits qu'ils renseignent au moment des plaintes<strong> amorce un cercle vertueux</strong> : cela les encourage à recueillir des données de qualité, condition nécessaire &#8211; datascience ou pas &#8211; à l'obtention de résultats pertinents.</span>
</p>
