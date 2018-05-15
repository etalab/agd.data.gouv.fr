---
id: 669
title: Les techniques standards appliquées é OpenSolarMap (1/3)
date: 2016-06-23T10:04:44+00:00
author: Michel Blancard
layout: post
guid: https://agd.data.gouv.fr/?p=669
permalink: /2016/06/23/les-techniques-standards-appliquees-a-opensolarmap-13/
kopa_nictitate_total_view:
  - "6"
categories:
  - Science des données
tags:
  - Datasciences
  - Energy
  - Machine-learning
  - OpenSolarMap
image: /wp-content/uploads/2016/04/lr.png
---
**Lorsqu'un algorithme simple ne convient pas, la deuxième étape d'un projet de machine learning est d'essayer des « grands classiques ». Ces algorithmes sont plus complexes d'un point de vue théorique, mais des implémentations toutes prètes existent etécette étape est généralementérapide é mettre en éuvre.**

# Régression Logistique

La [régression logistique](https://fr.wikipedia.org/wiki/R%C3%A9gression_logistique)éporte un nom déroutant puisque cette méthode est utilisée autant pour des problèmes de régression que de classification. De plus, le choix par Pierre Franéois Verhulstédu terme « logistique » est aujourd'hui un mystère. Pourtant, la régression logistique est sans doute la méthode la plus répandue pour traiter des problèmes de classification comme c'est le cas ici.

Il existe une multitude d'implémentations de la régression logistique. La méthode utilisée pour OpenSolarMap est celle de [Scikit-Learn](http://scikit-learn.org/).é Scikit-Learn est un ensemble d'implémentation en [langage Python](https://www.python.org/) d'algorithmes courants. Cette librairie maintenue par l'INRIA est très populaire partout dans le monde. Voir la documentation de l'implémentation : <http://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html>.

Entraéner puis tester un modèle de régression logistique requiert peu de code é écrire :

<pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title="">train_data, val_data, test_data = load.load_all_data(train_ids, val_ids, test_ids, l, color)
model = sklearn.linear_model.LogisticRegression(penalty='l2', C=1e10)
model.fit(train_data, train_labels)
predictions = model.predict(val_data)
err = (predictions != val_labels).sum() / len(val_labels)
</pre>

Passons en revue chaque ligne :

  1. Les données sont chargées dans les variablesé`train_data`, `val_data` eté`test_data`.éLa fonction `load.load_all_data()`, spécifique a notre problème,éprend en paramètre la liste des identifiants de toits é charger, la taille `l` des images voulue et le nombre de canaux de couleur voulus (rouge, vert et bleu ou noir et blanc). Les images de toitures sont séparées en 3 échantillons : 
      * Un échantillon d'apprentissage.
      * Un échantillon de test.
      * Un échantillon de validation.
  2. Un objet python encapsulantéun modèle de régression linéaire est créé. Les paramètres `penalty` et `C`éconfigurentéla régularisation. Laé[régularisation](https://en.wikipedia.org/wiki/Regularization_(mathematics))éest utile lorsque le nombre de features est comparable é la taille de l'échantillon. Ici, il y a plusieurs milliers d'exemples dans l'échantillon d'apprentissage et quelques centaines de features tout au plus. Pour simplifier, le paramètre `C` a une valeur très élevée (`1e10 = 10.000.000.000`) ce qui correspond é une régularisation négligeable.
  3. Le modèle est entraéné sur l'échantillon d'apprentissage. Le modèle a accès aux features (`train_data`) mais aussi aux labels (`train_labels`) pour pouvoir se corriger et s'améliorer.
  4. Le modèle fait des prédictions sur l'échantillon de test. Maintenant le modèle n'a pas accès aux labels.
  5. Le taux d'erreurs de la prédiction du modèle est calculé comme le quotient du nombre d'erreurs sur la taille de l'échantillon.

<div id="attachment_598" style="width: 310px" class="wp-caption alignright">
  <a href="https://agd.data.gouv.fr/wp-content/uploads/2016/04/lr.png"><img class="wp-image-598 size-medium" src="https://agd.data.gouv.fr/wp-content/uploads/2016/04/lr-300x209.png" alt="lr" width="300" height="209" srcset="https://agd.data.gouv.fr/wp-content/uploads/2016/04/lr-300x209.png 300w, https://agd.data.gouv.fr/wp-content/uploads/2016/04/lr.png 403w" sizes="(max-width: 300px) 100vw, 300px" /></a>
  
  <p class="wp-caption-text">
    Figure 1 : choix des hyperparamètres pour la régression logistique
  </p>
</div>

On choisit la taille des images `l` et le choix de couleurs (rouge, vert et bleu ou noir et blanc) en essayant plusieurs combinaison. La figure 1 montre que la taille qui donne les meilleurs résultats est de 6 pixels par 6 pixels. Le fait de tester successivement plusieurs hyper-paramètres (les paramètres, comme `l`, qui sont extérieurs au modèle de régression logistique et définis par le data-scientist) peut provoquer un phénomène appelé [surapprentissage](https://fr.wikipedia.org/wiki/Surapprentissage). Il est nécessaire de valider la performance sur un échantillon qui n'a été utilisé ni durant l'apprentissage ni durant la phase de test, l'[échantillon de validation](https://en.wikipedia.org/wiki/Test_set#Validation_set). Dans notre situation, le taux d'erreur sur l'échantillon de validation est de 12.5%.

&nbsp;

<h1 style="text-align: left;">
  Support Vector Machines
</h1>

Si la régression logistique a été développée dans la fin des années 60 par le statisticien David Cox et elle est maintenant considérée comme un outil de statistique classique, les « machines é vecteurs de support » sont développées depuis les années 90 et constituent encore un domaine de recherche très actif. Cette différence d'ège, ainsi que le fait que l'analyse mathématique de ces deux méthodes est très différente fait souvent oublier que les performances, tant en prédiction qu'en temps de calcul, sont souvent très semblables.

Passer de la régression logistique au [Support Vector Classifier (SVC)](http://scikit-learn.org/stable/modules/generated/sklearn.svm.LinearSVC.html)éest presque immédiat, il faut remplacer la ligne

<pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title="">model = sklearn.linear_model.LogisticRegression(penalty='l2', C=1e10)
</pre>

par la ligne

<pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title="">model = sklearn.svm.LinearSVC(penalty='l2', C=1e10, dual=False)
</pre>

Le paramètre `dual=False`écommande é la librairie Scikit-Learn de ne pas utiliser l'implémentation « duale », qui est appropriéeédans les cas oè le nombre de features est plus important que la taille de l'échantillon.

Le meilleur résultat est toujours obtenu avec une taille de 6 pixels par 6 pixels, mais cette fois-ci en couleurs (rouge, vert et bleu). Le résultat de l'étape de la validation est aussi de 12.5%.

<div id="attachment_599" style="width: 310px" class="wp-caption aligncenter">
  <a href="https://agd.data.gouv.fr/wp-content/uploads/2016/04/svm.png"><img class="wp-image-599 size-medium" src="https://agd.data.gouv.fr/wp-content/uploads/2016/04/svm-300x213.png" alt="svm" width="300" height="213" srcset="https://agd.data.gouv.fr/wp-content/uploads/2016/04/svm-300x213.png 300w, https://agd.data.gouv.fr/wp-content/uploads/2016/04/svm.png 396w" sizes="(max-width: 300px) 100vw, 300px" /></a>
  
  <p class="wp-caption-text">
    Figure 2 : choix des hyperparamètres pour la SVM
  </p>
</div>

# Quels sont les grands classiques ?

Pour beaucoup de problèmes de machine learning, il existe un ou plusieurséalgorithmes classiques é essayer en priorité. Pour aider é faire ce choix, le projet Scikit-Learn a édité un [arbre de décision](http://scikit-learn.org/stable/tutorial/machine_learning_map/index.html) très pratique :

[<img class="wp-image-600 size-large aligncenter" src="https://agd.data.gouv.fr/wp-content/uploads/2016/04/ml_map-1024x638.png" alt="ml_map" width="806" height="502" srcset="https://agd.data.gouv.fr/wp-content/uploads/2016/04/ml_map-1024x638.png 1024w, https://agd.data.gouv.fr/wp-content/uploads/2016/04/ml_map-300x187.png 300w" sizes="(max-width: 806px) 100vw, 806px" />](https://agd.data.gouv.fr/wp-content/uploads/2016/04/ml_map.png)
