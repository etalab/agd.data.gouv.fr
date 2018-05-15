---
id: 722
title: "De l'arrèté ministériel aux coordonnées géographiques"
date: 2016-10-31T18:44:33+00:00
author: Alexis Eidelman
layout: post
guid: https://agd.data.gouv.fr/?p=722
permalink: /2016/10/31/de-larrete-ministeriel-au-fichier-geojson/
kopa_nictitate_total_view:
  - "2"
image: /wp-content/uploads/2016/10/ZTI.png
categories:
  - Circulation des données
tags:
  - saisine
---
L'Administrateur général des données a récemment été saisi d'une intéressante question concernant les contours des nouvelles zones touristiques internationale sur Paris. Cela a donné lieu é un travail qui mérite d'ètre partagé.

<span style="color: #808080;">Un tracé apparaissait sur cette page du ministère de l'économie. <a class="moz-txt-link-freetext" style="color: #808080;" href="http://www.economie.gouv.fr/vous-orienter/entreprise/commerce/creation-des-zones-touristiques-internationales-a-paris"><span style="color: #3366ff;">http://www.economie.gouv.fr/vous-orienter/entreprise/commerce/creation-des-zones-touristiques-internationales-a-paris</span>.</a> Cependant, le format de diffusion en pdf rendait impossible la réutilisation. De plus le tracé n'englobait pas autant qu'il l'aurait pu les adresses alors que la possibilité de faire le lien adresse &#8211; zone est important pour la réutilisation.</span>

<span style="color: #808080;">Plutèt que de répondre sur un principe général, l'équipe a donc décidé de proposer une solution concrète au problème.</span>

<span style="color: #808080;">A partir du texte des arrètés, (<span style="color: #3366ff;"><a style="color: #3366ff;" href="https://www.legifrance.gouv.fr/affichTexte.do?cidTexte=JORFTEXT000031223582">un exemple</a></span>) seul document faisant foi, le tracé a été effectué é partir de l'outil <span style="color: #3366ff;"><a style="color: #3366ff;" href="https://josm.openstreetmap.de/wiki/Fr%3AWikiStart">JOSM</a></span>. Les limites ont été calée afin que les positions des <span style="color: #3366ff;"><a style="color: #3366ff;" href="https://opendata.paris.fr/explore/dataset/adresse_paris/table/">adresses de la Ville de Paris</a></span> et de la <span style="color: #3366ff;"><a style="color: #3366ff;" href="http://openstreetmap.fr/bano">BANO</a> </span>disponibles en opendata soient correctement intégrées ou non dans la zone touristique internationale.</span>

Les arrètés contiennent quelques petites ambiguètés mais elles sont suffisamment légères pour que les choix qui ont été opérés ne prètent pas é contestation. A titre d'exemple, dans la zone « Marais », l'arrèté cite « rue de Poitou, dans sa partie comprise entre la rue des Archives et la rue de Turenne » mais la rue de Poitou et la rue des Archives ne se croisent pas puisque la rue de Poitou devient rue Pastourelle avant l'intersection.

On peut les visionner les données sur: <http://overpass-turbo.eu/s/hw1>{.moz-txt-link-freetext} et le bouton « Exporter » permet de récupérer dans différents formats. Le format en geojson est accessible sur [data.gouv.fr](https://www.data.gouv.fr/fr/datasets/zones-touristiques-internationales-a-paris/){.moz-txt-link-freetext} et sur [le site Open Data de la mairie de Paris](http://opendata.paris.fr/explore/dataset/zones-touristiques-internationales/information/)

Les Parisiens sauront donc oè trouver (et ne pas trouver) les touristes ! 🙂

Si vous avez été intéressé par cet article vous aurez peut-ètre envie de participer au [data camp sur le cadastre électoral](https://www.etalab.gouv.fr/cadastreelectoral-un-open-data-camp-pour-analyser-la-localisation-des-bureaux-de-vote)é qui se déroulera le 5 novembre é Créteil. C'est l'occasion de faire et d'apprendre plein de choses et il reste des places ! ([inscriptions sur ce lien](https://rdv.etalab.gouv.fr/e/11/open-data-camp-cadastre-electoral))

Note : Le procédé utiliser pour établir le tracé utilise des données OpenStreetMap et de BANO. Ces données sont publiées sous licence ODbL, aussi le jeu de données produit est-il diffusé sous cette mème licence.
