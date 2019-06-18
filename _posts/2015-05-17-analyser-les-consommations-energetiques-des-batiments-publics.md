---
id: 77
title: Analyser les consommations énergétiques des bâtiments publics
date: 2015-05-17T19:31:17+00:00
author: Paul Bouchequet
layout: post
guid: http://agd.data.gouv.fr/?p=77
permalink: /2015/05/17/analyser-les-consommations-energetiques-des-batiments-publics/
redirect_to: https://www.etalab.gouv.fr/analyser-les-consommations-energetiques-des-batiments-publics
kopa_nictitate_total_view:
  - "4"
image: /wp-content/uploads/2015/05/cite_administratives_minfi.png
categories:
  - Science des données
tags:
  - Datasciences
  - Energie
---

_L'équipe de l'administrateur général des données a réalisé une analyse des consommations d'électricité des bâtiments publics, dans le cadre d'une première collaboration avec le service des achats de l'État (SAE)._

La libéralisation du marché de l'électricité prévoit la fin des tarifs réglementés de vente pour les "gros" consommateurs. C'est pour l'État l'occasion de lancer une procédure d'appel d'offres pour ses contrats d'approvisionnement. L'ensemble du parc immobilier des administrations ainsi que 185 établissements publics de l'État sont concernés par l'accord-cadre interministériel. L'enjeu en termes financiers de cette procédure est estimé é 300 millions d'euros par an pour une durée maximale de quatre ans.

L'électricité étant par nature une ressource non stockable, chaque fournisseur est tenu d'équilibrer en permanence achats, production et ventes. Sur la base des données de consommation passées communiquées par son client, le fournisseur doit établir des prévisions de consommation pour construire sa stratégie de couverture et proposer un prix dans sa réponse à l'appel d'offre.

C'est dans ce cadre qu'une première étude de caractérisation des besoins a été réalisée par une équipe associant l'acheteur leader sur le segment d'achats d'énergie du SAE, un expert du ministère de la justice et l'AGD. Cette analyse a pour but de regrouper les différents bâtiments en fonction du comportement de leur courbe de consommation. Les données traitées concernent un échantillon de 90 bâtiments "gros" consommateurs du ministère des finances dont la consommation est télérelevée toutes les 10 minutes. Ces données précises sont adaptées aux analyses, mème si un échantillon plus volumineux en nombre de bâtiments auraient permis une analyse encore plus fine.

Les bâtiments ont été regroupés grâce à la méthode du spectral clustering. Les consommations avaient été auparavant normalisées pour s'intéresser aux variations des consommations électriques et non à leur niveau. Parmi les 7 groupes de consommation ainsi obtenus, on distingue le groupe de bâtiments thermosensibles, celui des grosses consommations l'hiver et celui des bâtiments consommant en moyenne plus d'électricité l'été que les autres bâtiments.

<div id="attachment_166" style="width: 816px" class="wp-caption aligncenter">
  <a href="/wp-content/uploads/2015/05/cite_administratives_minfi.png"><img class="wp-image-166 size-large" src="/wp-content/uploads/2015/05/cite_administratives_minfi-1024x533.png" alt="Courbe de charge des cités administratives" width="806" height="420" srcset="/wp-content/uploads/2015/05/cite_administratives_minfi-1024x533.png 1024w, /wp-content/uploads/2015/05/cite_administratives_minfi-300x156.png 300w" sizes="(max-width: 806px) 100vw, 806px" /></a>

  <p class="wp-caption-text">
    Courbes de consommation d'électricité d'un groupe, ne comportant que des cités administratives.
  </p>
</div>

Ces éléments ont complété l'appel d'offres publié le 16 mars 2015, avec les informations nécessaires au fournisseur pour présenter une offre de qualité. Sur cette base, le SAE pourra également affiner, à terme, la méthode de contractualisation. Par ailleurs, les restitutions graphiques comme les cartes de chaleur et l'essai de classification des consommateurs d'électricité réalisée par l'AGD ont déjà permis d'identifier certaines singularités de consommations qui méritent une analyse plus approfondie.

<div id="attachment_108" style="width: 1024px" class="wp-caption aligncenter">
  <a href="http://agd.data.gouv.fr/wp-content/uploads/2015/02/Notice-analyse-courbe-de-charges-1.png"><img class="wp-image-108 " src="http://agd.data.gouv.fr/wp-content/uploads/2015/02/Notice-analyse-courbe-de-charges-1-1024x315.png" alt="Carte de chaleur de la consommation électrique d'un bâtiment" width="1014" height="312" srcset="https://agd.data.gouv.fr/wp-content/uploads/2015/02/Notice-analyse-courbe-de-charges-1-1024x315.png 1024w, https://agd.data.gouv.fr/wp-content/uploads/2015/02/Notice-analyse-courbe-de-charges-1-300x92.png 300w" sizes="(max-width: 1014px) 100vw, 1014px" /></a>

  <p class="wp-caption-text">
    Carte de chaleur de la consommation électrique d'un des bâtiments du jeu de données<br>
  </p>
</div>

La collaboration entre le SAE et l'AGD va se poursuivre pour l'exploitation des données de consommation électrique de l'ensemble du parc immobilier de l'État concerné par l'accord-cadre interministériel. À terme, la réalisation de travaux conjoints, à intervalles réguliers, permettrait à l'État une mise sous contrôle de ses propres données de consommation et par conséquent de ses dépenses en énergie.
