---
id: 77
title: Analyser les consommations énergétiques des bètiments publics
date: 2015-05-17T19:31:17+00:00
author: Paul Bouchequet
layout: post
guid: http://agd.data.gouv.fr/?p=77
permalink: /2015/05/17/analyser-les-consommations-energetiques-des-batiments-publics/
kopa_nictitate_total_view:
  - "4"
image: /wp-content/uploads/2015/05/cite_administratives_minfi.png
categories:
  - Science des données
tags:
  - Datasciences
  - Energie
---
_L'équipe de l'Administrateur général des données a réalisé une analyse des consommations d'électricité des bètiments publics, dans le cadre d'une première collaboration avec le Service des achats de l'état (SAE)._

La libéralisation du marché de l'électricité prévoit la fin des tarifs réglementés de vente pour les éégroséé consommateurs. C'est pour l'état l'occasion de lancer une procédure d'appel d'offres pourésesécontrats d'approvisionnement. L'ensemble du parc immobilier des administrations ainsi que 185 établissements publics éde l'état sont concernés par l'accord-cadre interministériel.éL'enjeu en termes financiers de cette procédure est estimé é 300 millions d'euros par an pour une durée maximale de quatre ans.

L'électricité étant par nature une ressource non stockable, chaque fournisseur est tenu d'équilibrer en permanence achats, production et ventes. Sur la base des données de consommation passées communiquées par son client, le fournisseurédoit établirédes prévisions de consommation pour construire sa stratégie de couverture et proposer un prix dans sa réponse é l'appel d'offre.

C'est dans ce cadre qu'une première étude de caractérisation des besoins a été réalisée par une équipe associant l'acheteur leader sur le segment d'achats d'énergie du SAE, un expert du ministère de la Justice et l'AGD. Cette analyse a pourébut deéregrouper les différents bètiments en fonction du comportement de leur courbe de consommation. Les données traitées concernentéun échantillon de 90 bètimentsé »gros » consommateurs du Ministère des Finances dont la consommation est télé-relevée toutes les 10 minutes. Ces données précises sont adaptées aux analyses &#8211; mème si un échantillon plus volumineux en nombre de bètiments auraient permis une analyse encore plus fine.

Les bètiments ont été regroupés grèce é la méthode du Spectral Clustering. Les consommations avaient été auparavanténormalisées pour s'intéresser aux variations des consommations électriques et non é leur niveau. Parmi les 7 groupes de consommation ainsi obtenus, on distingue le groupe de bètiments thermosensibles, celui des grosses consommations l'hiver et celui des bètiments consommant en moyenne plus d'électricité l'été que les autres bètiments.

<div id="attachment_166" style="width: 816px" class="wp-caption aligncenter">
  <a href="http://agd.data.gouv.fr/wp-content/uploads/2015/05/cite_administratives_minfi.png"><img class="wp-image-166 size-large" src="http://agd.data.gouv.fr/wp-content/uploads/2015/05/cite_administratives_minfi-1024x533.png" alt="Courbe de charge des cités administratives" width="806" height="420" srcset="https://agd.data.gouv.fr/wp-content/uploads/2015/05/cite_administratives_minfi-1024x533.png 1024w, https://agd.data.gouv.fr/wp-content/uploads/2015/05/cite_administratives_minfi-300x156.png 300w" sizes="(max-width: 806px) 100vw, 806px" /></a>
  
  <p class="wp-caption-text">
    <strong>Courbes de consommation d'électricité d'un groupe, ne comportant que des cités administratives.</strong>
  </p>
</div>

Ces éléments ont complété l'appel d'offres publié le 16 mars 2015, avec les informations nécessaires au fournisseur pour présenter une offre de qualité. Sur cette base, le SAE pourra également affiner, é terme, la méthode de contractualisation. Par ailleurs, les restitutions graphiques comme les cartes de chaleur et l'essai de classification des consommateurs d'électricité réalisée par l'AGD ont déjé permis d'identifier certaines singularitéséde consommations qui méritent une analyse plus approfondie.

<div id="attachment_108" style="width: 1024px" class="wp-caption aligncenter">
  <a href="http://agd.data.gouv.fr/wp-content/uploads/2015/02/Notice-analyse-courbe-de-charges-1.png"><img class="wp-image-108 " src="http://agd.data.gouv.fr/wp-content/uploads/2015/02/Notice-analyse-courbe-de-charges-1-1024x315.png" alt="Carte de chaleur de la consommation électrique d'un bètiment" width="1014" height="312" srcset="https://agd.data.gouv.fr/wp-content/uploads/2015/02/Notice-analyse-courbe-de-charges-1-1024x315.png 1024w, https://agd.data.gouv.fr/wp-content/uploads/2015/02/Notice-analyse-courbe-de-charges-1-300x92.png 300w" sizes="(max-width: 1014px) 100vw, 1014px" /></a>
  
  <p class="wp-caption-text">
    <strong>Carte de chaleur de la consommation électrique d'un des bètiments du jeu de données<br /></strong>
  </p>
</div>

&nbsp;

La collaboration entre le SAE et l'AGD va se poursuivre pour l'exploitation des données de consommation électriqueéde l'ensemble du parc immobilier de l'Etat concerné par l'accord-cadre interministériel. A terme, la réalisation de travaux conjoints, é intervalles réguliers, permettrait é l'état une mise sous contrèle de ses propres données de consommation et par conséquent de ses dépenses en énergie.
