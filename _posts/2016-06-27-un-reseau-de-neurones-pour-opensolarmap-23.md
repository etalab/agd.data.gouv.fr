---
id: 685
title: Un réseau de neurones pour OpenSolarMap (2/3)
date: 2016-06-27T14:26:28+00:00
author: Michel Blancard
layout: post
guid: https://agd.data.gouv.fr/?p=685
permalink: /2016/06/27/un-reseau-de-neurones-pour-opensolarmap-23/
kopa_nictitate_total_view:
  - "35"
categories:
  - Science des données
tags:
  - Datasciences
  - Energy
  - Machine-learning
  - OpenSolarMap

image: /wp-content/uploads/2016/04/neurone-1.png
excerpt: Après avoir essayé un algorithme très simple, puis un ou plusieurs algorithmes classiques, il est parfois (mais pas toujours) nécessaire de mettre en place un algorithme spécialisé dans le problème à résoudre. Les réseaux de neurones sont une catégorie d'algorithmes qui ont fait leurs preuves de manière spectaculaire dans le domaine du traitement d'images.
---
**Après avoir essayé un algorithme très simple, puis un ou plusieurs algorithmes classiques, il est parfois (mais pas toujours) nécessaire de mettre en place un algorithme spécialisé dans le problème é résoudre. Les réseaux de neurones sont une catégorieéd'algorithmes qui ont fait leurs preuves de manière spectaculaire dans le domaine du traitement d'images.**

# Introduction

Au delé de l'effet de mode dont ils bénéficient, les réseaux de neurones constituent bel et bien une avancéeémajeure en traitement d'images et dans bien d'autresédomaines. Ce champ de rechercheéreprésente une proportion importante des articles parues dans les revues de référence en machine learning : <a href="https://nips.cc/Conferences/2015/AcceptedPapers">NIPS</a> et <a href="http://jmlr.org/proceedings/papers/v37/">ICML</a>. Le domaine jouit également d'une pleine reconnaissance académique comme l'illustre la chaire annuelle de l'INRIA au Collège de France en <a href="http://www.college-de-france.fr/site/yann-lecun/">« Informatique et sciences numériques »</a> consacrée par Yann LeCun aux réseaux neuronaux. Cette chaire, cours et séminaires inclus, constitue d'ailleurs une excellente introduction aux techniques des réseaux neuronaux, parmi les multiples ressources disponibles librement sur Internet.

Les réseaux de neurones sont étudiés depuis les années 50 avec l'invention du <a href="https://fr.wikipedia.org/wiki/Perceptron">perceptron</a>. Mais ceux qui bouleversent la communauté du machine learning depuis 2011 se dénomment plus précisément « réseaux de neurones profonds é convolution » (« deep convolutional neural networks », abrégé parfois enéCNN pour Convolutional Neural Networks ou encore ConvNets) :

<li style="text-align: justify;">
  <strong>neurone</strong> : Mème s'il y a une lointaine analogie entre les neurones biologiques et les neurones informatiques, ils constituent deux domaines d'étude é ne pas confondre. Un neurone informatique prend en entrée plusieurs valeurs numériques et applique une fonction é ces entrées. Le résultat numérique de cette fonction constitue l'unique sortie du neurone. Le neurone <a href="https://en.wikipedia.org/wiki/Rectifier_(neural_networks)">Rectified Linear Unit</a>é(ReLU)éest majoritairement employé : chaque entrée estémultipliée par un coefficient (ou poids) puis cette somme est renvoyée si elle est positive, zéro est renvoyé sinon. <p>
    <div id="attachment_681" style="width: 778px" class="wp-caption aligncenter">
      <a href="https://agd.data.gouv.fr/wp-content/uploads/2016/04/neurone-1.png"><img class="wp-image-681 size-full" src="https://agd.data.gouv.fr/wp-content/uploads/2016/04/neurone-1.png" alt="neurone" width="768" height="480" srcset="https://agd.data.gouv.fr/wp-content/uploads/2016/04/neurone-1.png 768w, https://agd.data.gouv.fr/wp-content/uploads/2016/04/neurone-1-300x188.png 300w" sizes="(max-width: 768px) 100vw, 768px" /></a>
      
      <p class="wp-caption-text">
        Figure 1 : neurone de type ReLU é 3 entrées.
      </p>
    </div></li> 
    
    <li style="text-align: justify;">
      <strong>réseau</strong> : Les neurones sont disposés en un réseau qui prend la forme de plusieurs couches successives. La première couche prend en entrée les valeurs de l'image (ou d'un autre type d'entrée comme du texte ou du son). Les sorties de la première couche constituent les entrées de la deuxième couche, etc. Les sorties de la dernière couche sontéles sorties du réseau, mais les valeurs numériques qui transitent entre les couches sont cachées é l'utilisateur.éDe lé vient en partie leur réputation d'ètre des « boétes noires ». <p>
        <div id="attachment_682" style="width: 634px" class="wp-caption aligncenter">
          <a href="https://agd.data.gouv.fr/wp-content/uploads/2016/04/réseau.png"><img class="wp-image-682 size-full" src="https://agd.data.gouv.fr/wp-content/uploads/2016/04/réseau.png" alt="réseau" width="624" height="528" /></a>
          
          <p class="wp-caption-text">
            Figure 2 : réseau de neurones é 3 couches
          </p>
        </div></li> 
        
        <li style="text-align: justify;">
          <strong>convolution </strong><em>(paragraphe technique é lire en seconde lecture)</em> : Les <a href="https://en.wikipedia.org/wiki/Convolutional_neural_network">réseaux é convolution</a> opèrent généralement sur des images. La première couche de neurones est de la mème forme que l'image en entrée. La sortie de cette première couche, comme toutes les sorties intermédiaires, forment des images.éAu sein d'une couche de neurones, les paramètres de chaque neurones sont choisis de telle sorte que la couche applique un filtrage linéaire puis une rectification. Un filtrage linéaire est la convolution entre une image d'entrée et un filtre linéaire. Un filtre linéaire, dans le cas du traitement d'images, se représente come une petite image, typiquement de taille 3 par 3 pixels ou 5 par 5. Les réseaux é convolution ont l'avantage de tirer partie de la structure géométrique de l'image d'entrée. De plus, chaque couche de neurones est paramétrée par un filtre linéaire qui est beaucoup plus simple é apprendre que dans le cas général. Par exemple, pour une image d'entrée de 224 par 224 pixel en noir et blanc, une couche de neurones de la mème taille est composé de 224 éé224 neurones et si chaque neurone est connecté é chaque pixel d'entrée, il y a 224 éé224 paramètres par neurones. Cela fait un total de 224 éé224 éé224 éé224 = 2.517.630.976éparamètres pour cette seule couche. Il faudrait donc des milliards d'images pour faire apprendre correctement un tel réseau. En comparaison, paramétrer la couche de neurones par un filtre de 3 éé3 pixels ne requiert d'apprendre que 9 valeurs numériques. Concrètement, cela revient é mettreéla majorité des poids des neurones é zéro, et é partager tous les poids restants entre les neurones de la couche. Dans un réseau é convolution, des étapes de réduction de la taille de l'image s'intercalent entre les couches de neurones. Pour le réseau LeNet 5, deux étapes de réduction, appelées « subsampling » alternent avec les deux étapes de convolution. Les dernières couchent perdent la structure géométrique en dépliant l'image sur une dimension, mais le nombre de paramètres é apprendre est raisonnable du fait de la petite taille des images. Enfin, il faut préciser que, de la mème manière qu'une image d'entrée peut contenir plusieurs canaux de couleur (rouge, vert et bleu par exemple), les images intermédiaires se composent de plusieurs canaux. Dans le cas de LeNet 5, les images intermédiaires se composent de 6 puis de 16 canaux. Au fil de l'apprentissage du réseau, chaque canal va se spécialiser dans la reconnaissance d'une forme géométrique particulière.
        </li>
        <li style="text-align: justify;">
          <strong>profond</strong> : éLes réseaux de neurones traditionnels, étudiés dans les années 70, utilisaient entre 1 et 3 couches de neurones. On parle de réseaux profonds pour parler des architectures avec un nombre élevés de couches qui peut dépasser la centaine ! Les couches proches de l'image d'entrée se spécialisent dans la détection de features géométriques très simplesé(des coins, des lignes&#8230;) alors les couches finales détectent des features abstraites qui dépendent de l'usage du réseau (des lettres pour un réseau de reconnaissance d'écriture, des objets, des espèces d'animaux&#8230;).
        </li></ul> 
        
        <div id="attachment_604" style="width: 706px" class="wp-caption aligncenter">
          <a href="https://agd.data.gouv.fr/wp-content/uploads/2016/04/lenet5.png"><img class="wp-image-604 size-full" src="https://agd.data.gouv.fr/wp-content/uploads/2016/04/lenet5.png" alt="lenet5" width="696" height="204" srcset="https://agd.data.gouv.fr/wp-content/uploads/2016/04/lenet5.png 696w, https://agd.data.gouv.fr/wp-content/uploads/2016/04/lenet5-300x88.png 300w" sizes="(max-width: 696px) 100vw, 696px" /></a>
          
          <p class="wp-caption-text">
            Fgure 3 : réseau de neurones LeNet 5
          </p>
        </div>
        
        <p style="text-align: justify;">
          Comme tous les algorithmes dits supervisés, les réseaux de neurones sont « appris » sur un échantillon de données d'exemples labellisés. La méthode d'apprentissage utilisée, nommée <a href="https://en.wikipedia.org/wiki/Backpropagation">backpropagation</a>,éva modifier petit é petitéles paramètreséde chaque couche pour augmenter la qualité des prédictions jusqu'é atteindre une situation (localement) optimale. Une fois la phase d'apprentissage terminée, le réseauéest capable de faire des prédictions sur de nouvelles images.
        </p>
        
        <p style="text-align: justify;">
          Les réseaux de neurones présentent des performances spectaculaires et inattendues. Une des enjeux théorique actuel estéde comprendreéces performances et de les confirmer par des garanties théoriques. C'est par exemple l'objet des recherches actuelle de Stéphane Mallat qui travaille sur la <a href="http://www.di.ens.fr/data/scattering/math/">méthode de scattering</a>,éapparentée aux réseaux de neurones.
        </p>
        
        <h1>
          Librairie, réseau et code utilisés
        </h1>
        
        <h2>
          Librairie de deep-learning
        </h2>
        
        <p style="text-align: justify;">
          Les librairies de deep-learning <a href="http://deeplearning.net/software_links/">ne manquent pas</a>. La difficulté est de choisir l'outil qui répond le mieux aux besoinsédu projet. Pour répondre aux besoins d'OpenSolarMap, l'outil idéal devra :
        </p>
        
        <ul>
          <li style="text-align: justify;">
            ètre utilisable facilement et rapidement, c'est-é-dire gérer lui-mème la totalité des calculs
          </li>
          <li style="text-align: justify;">
            laisser la possibilité de faire des modifications simples sur le réseau utilisé
          </li>
          <li style="text-align: justify;">
            ètre en open source pour pouvoir ètre essayéédans l'heure (et passer é un autre outil s'il ne correspond pas parfaitement)
          </li>
          <li style="text-align: justify;">
            proposer une API en python car c'est le langage que nous utilisons majoritairement é l'AGD
          </li>
          <li style="text-align: justify;">
            rassembler une communauté active, pour disposer d'exemples d'utilisation, pour disposer de nombreuses questions/réponses suré<a href="http://stackoverflow.com/">stackoverflow.com</a>, pour pouvoir compter sur l'aide de la communauté en dernier recours
          </li>
          <li style="text-align: justify;">
            en bonus, pouvoir utiliser la <a href="https://en.wikipedia.org/wiki/General-purpose_computing_on_graphics_processing_units">puissance de calcul des GPU</a>.
          </li>
        </ul>
        
        <p style="text-align: justify;">
          Parmi d'autres solutions qui auraient satisfait ces critères, j'ai choisi <a href="http://keras.io/">Keras</a>ésur les recommandations d'un confrère data-scientist. Je n'ai pas eu é regretter ce choix, mais si Keras n'avait pas convenu, j'aurais sans doute testé les outils <a href="http://caffe.berkeleyvision.org/">Caffe</a>, <a href="https://github.com/Lasagne/Lasagne">Lasagne</a>éou le très populaire <a href="http://torch.ch/">Torch</a>émème s'il est écrit en <a href="https://fr.wikipedia.org/wiki/Lua">lua</a>.
        </p>
        
        <h2>
          Réseau de neurones VGG16
        </h2>
        
        <p style="text-align: justify;">
          Concevoir un réseau de neurones est une tèche compliquée qui nécessite une expérience approfondie. En revanche, utiliser une réseau de neurones déjé prèt est beaucoup plus simple et rapide é mettre en éuvre. Le « transfer learning » une technique standard expliquée dans cesé<a href="http://cs231n.github.io/transfer-learning/">notes</a>édu <a href="http://vision.stanford.edu/teaching/cs231n/">cours de vision CS231n de Standford</a>.
        </p>
        
        <p style="text-align: justify;">
          Il y a déjé de nombreux réseaux pré-entraénés disponibles. Le projet <a href="https://github.com/BVLC/caffe/wiki/Model-Zoo">Model-Zoo</a> de l'université de Berkeley est une liste de ces réseaux qui est d'un grand usage pour faire ce choix. Les réseaux listés par Model-Zoo sont proposés en Caffe, mais la plupart des modèles sont directement utilisables avec d'autres librairies. J'ai choisi arbitrairement le célèbre <a href="http://www.robots.ox.ac.uk/~vgg/research/very_deep/">réseau é 16 couches VGG16</a>édu <a href="http://www.robots.ox.ac.uk/~vgg/">Visual Geometry Group</a> de l'université d'Oxford utilisé lors de la competitioné<a href="http://www.image-net.org/challenges/LSVRC/2014/">ILSVRC de 2014</a>é(ImageNet 2014). Il s'agit d'un réseau généraliste. D'autres réseaux auraient pu convenir aussi bien et peut-ètre mème mieux. Ce réseau est directement utilisable avec Keras en utilisant le GitHub Gist suivant :é<a href="https://gist.github.com/baraldilorenzo/07d7802847aaad0a35d3">https://gist.github.com/baraldilorenzo/07d7802847aaad0a35d3</a>
        </p>
        
        <pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title="">
model = Sequential()
model.add(ZeroPadding2D((1,1),input_shape=(3,224,224)))
model.add(Convolution2D(64, 3, 3, activation='relu'))
model.add(ZeroPadding2D((1,1)))
model.add(Convolution2D(64, 3, 3, activation='relu'))
model.add(MaxPooling2D((2,2), strides=(2,2)))

model.add(ZeroPadding2D((1,1)))
model.add(Convolution2D(128, 3, 3, activation='relu'))
model.add(ZeroPadding2D((1,1)))
model.add(Convolution2D(128, 3, 3, activation='relu'))
model.add(MaxPooling2D((2,2), strides=(2,2)))

model.add(ZeroPadding2D((1,1)))
model.add(Convolution2D(256, 3, 3, activation='relu'))
model.add(ZeroPadding2D((1,1)))
model.add(Convolution2D(256, 3, 3, activation='relu'))
model.add(ZeroPadding2D((1,1)))
model.add(Convolution2D(256, 3, 3, activation='relu'))
model.add(MaxPooling2D((2,2), strides=(2,2)))

model.add(ZeroPadding2D((1,1)))
model.add(Convolution2D(512, 3, 3, activation='relu'))
model.add(ZeroPadding2D((1,1)))
model.add(Convolution2D(512, 3, 3, activation='relu'))
model.add(ZeroPadding2D((1,1)))
model.add(Convolution2D(512, 3, 3, activation='relu'))
model.add(MaxPooling2D((2,2), strides=(2,2)))

model.add(ZeroPadding2D((1,1)))
model.add(Convolution2D(512, 3, 3, activation='relu'))
model.add(ZeroPadding2D((1,1)))
model.add(Convolution2D(512, 3, 3, activation='relu'))
model.add(ZeroPadding2D((1,1)))
model.add(Convolution2D(512, 3, 3, activation='relu'))
model.add(MaxPooling2D((2,2), strides=(2,2)))

model.add(Flatten())
model.add(Dense(4096, activation='relu'))
model.add(Dropout(0.5))
model.add(Dense(4096, activation='relu'))
model.add(Dropout(0.5))
model.add(Dense(1000, activation='softmax'))
</pre>
        
        <p style="text-align: justify;">
          La première ligne définit un modèle séquentiel. D'autre architectureséplus compliquées existent, mais le réseau VGG16 est un empilement de couches dont chaque couche prend en entrée le résultat de la couche précédente. les lignes
        </p>
        
        <pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title="">
model.add(Convolution2D(xxx, 3, 3, activation='relu'))
</pre>
        
        <p style="text-align: justify;">
          définissent des couches de neurones ReLU avec une taille de filtre de 3 par 3 pixels et un nombre de canaux de 34, 128, 256 ou 512. Les lignes
        </p>
        
        <pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title="">
model.add(MaxPooling2D((2,2), strides=(2,2)))
</pre>
        
        <p style="text-align: justify;">
          définissent les étapes de réduction de la taille de l'image le long du réseau. La méthode Max Pooling est utilisée et chaque étape divise par 2 la taille. Les lignes
        </p>
        
        <pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title="">
model.add(ZeroPadding2D((1,1)))
</pre>
        
        <p style="text-align: justify;">
          sont un détail d'implémentation. Pour compenser la taille du filtre de 3 pixels, une bordure de 1 pixel est ajouté é l'image d'entrée avant chaque convolution pour que la sortie de la convolution soit de mème taille. Enfin, le dernier bloc définit 3 couches de neurones fully-connected.
        </p>
        
        <p style="text-align: justify;">
          La taille d'entrée spécifiée est 224 par 224 pixels (par 3 canaux). Chaque couple Zero Padding / Convolution ne modifie pas la taille (éventuellement le nombre de canaux) et chaque Max Pooling divise la taille par 2 (sans modifier le nombre de canaux). On peut en déduire que l'opération Flatten prend en entrée une image de 7 par 7 pixels avec 512 canaux et renvoie un vecteur de taille 25.088. Les deux couches suivantes comptent 4096 neurones puis la dernière en compte 1000, qui correspondent aux <a href="http://image-net.org/challenges/LSVRC/2014/browse-synsets">1000 classes é prédire pour la compétition ImageNet</a>.
        </p>
        
        <h1>
          Modification du réseau
        </h1>
        
        <p style="text-align: justify;">
          Le réseau a été entraéné pour classer une image parmi 1000 classes de la compétition ImageNet et non pas pour distinguer l'orientation des toitures. Mais une propriété des réseaux de neurones est qu'il sont également très efficace pour s'adapter é des problèmes voisins. Seules les dernières couches sont spécialisées dans la tèche é accomplir tandis que les premières couches résolvent des problèmes de détection très généraux. Le transfert learning utilise cet avantage pour utiliser très rapidement un réseau pour une nouvelle tèche. La méthode la plus simple, sans fine-tuning, a été utilisée pour OpenSolarMap.
        </p>
        
        <h2>
          Changement de la taille d'entrée
        </h2>
        
        <p style="text-align: justify;">
          Le réseau VGG16 prend en entrée des images de taille 224 par 224, or les images de toits ont une taille moyenne de 95 par 93 pixels (voir figure 4). On a le choix d'agrandir les images avant d'appliquer le réseau, ou de changer la taille d'entrée du réseau vers une valeur plus proche de la taille moyenne. La première approche fournirait des images majoritairementéfloues au réseau, c'est pourquoi j'ai choisi la secondeéapproche. La taille de 96 par 96 est idéale, car après les 5 étapes de réduction, la taille de l'image intermédiaire tombe « juste » sur 3 par 3 pixels.
        </p>
        
        <p style="text-align: justify;">
          La ligne 2 du gist est remplacée par :
        </p>
        
        <pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title="">
model.add(ZeroPadding2D((1,1),input_shape=(3,96,96)))
</pre>
        
        <div id="attachment_610" style="width: 310px" class="wp-caption aligncenter">
          <a href="https://agd.data.gouv.fr/wp-content/uploads/2016/04/size.png"><img class="wp-image-610 size-medium" src="https://agd.data.gouv.fr/wp-content/uploads/2016/04/size-300x298.png" alt="size" width="300" height="298" srcset="https://agd.data.gouv.fr/wp-content/uploads/2016/04/size-300x298.png 300w, https://agd.data.gouv.fr/wp-content/uploads/2016/04/size-150x150.png 150w, https://agd.data.gouv.fr/wp-content/uploads/2016/04/size.png 396w, https://agd.data.gouv.fr/wp-content/uploads/2016/04/size-80x80.png 80w, https://agd.data.gouv.fr/wp-content/uploads/2016/04/size-118x118.png 118w, https://agd.data.gouv.fr/wp-content/uploads/2016/04/size-32x32.png 32w, https://agd.data.gouv.fr/wp-content/uploads/2016/04/size-64x64.png 64w, https://agd.data.gouv.fr/wp-content/uploads/2016/04/size-96x96.png 96w, https://agd.data.gouv.fr/wp-content/uploads/2016/04/size-128x128.png 128w" sizes="(max-width: 300px) 100vw, 300px" /></a>
          
          <p class="wp-caption-text">
            Figure 4 : répartition des images de toits par taille (x, y)
          </p>
        </div>
        
        <h2>
          Transfer learning
        </h2>
        
        <p style="text-align: justify;">
          Les dernières couches sont spécifiques au concours ImagetNet et ne sont pas d'utilité ici. Ils sont donc retirés et le dernier bloc est remplacé par
        </p>
        
        <pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title="">
model.add(Flatten())
</pre>
        
        <p style="text-align: justify;">
          Le choix d'enlever 3 couches est arbitraire. La seule contrainte é respecter estéde conserver un nombre de features raisonnables, inférieur é 10.000. Avec ce choix, on compte alors 3 x 3 x 512 = 4608 featutres en sortie du réseau. Ce n'est pas une prédiction de la classe, mais ces features peuvent ètre utilisées par un classifieur comme une régression linéaire.
        </p>
        
        <h1>
          Résultats
        </h1>
        
        <p style="text-align: justify;">
          Les 4608 features calculées par le réseau alimentent un modèle de régression logistique, régularisé cette fois. Le paramètre de régularisation varie et le taux d'erreur (figure 5) affiche une classique courbe en U du <a href="https://fr.wikipedia.org/wiki/Dilemme_biais-variance">dilemme biais-variance</a>. C'est la valeur qui donne le meilleur résultat qui est retenue.éLa force de la régularisation est un hyperparamètre, donc il est indispensable de calculer la performance sur un échantillon de validation. Le taux d'erreur sur cet échantillon est de 7%.
        </p>
        
        <div id="attachment_611" style="width: 310px" class="wp-caption aligncenter">
          <a href="https://agd.data.gouv.fr/wp-content/uploads/2016/04/regul_cnn_lr.png"><img class="wp-image-611 size-medium" src="https://agd.data.gouv.fr/wp-content/uploads/2016/04/regul_cnn_lr-300x213.png" alt="regul_cnn_lr" width="300" height="213" srcset="https://agd.data.gouv.fr/wp-content/uploads/2016/04/regul_cnn_lr-300x213.png 300w, https://agd.data.gouv.fr/wp-content/uploads/2016/04/regul_cnn_lr.png 402w" sizes="(max-width: 300px) 100vw, 300px" /></a>
          
          <p class="wp-caption-text">
            Figure 5 : taux d'erreur en fonction de la force de la régularisation
          </p>
        </div>
        
        <p style="text-align: justify;">
          Ce taux d'erreur est bien moins bon que ce qu'il serait possible d'obtenir avec des méthodes « state-of-the-art ». Tout d'abord, il faudraitétester d'autres réseaux que le VGG16, essayer différents choix de couches é enlever voire faire duéfine-tuning&#8230; Ici, il s'agissait surtout de démontrer qu'il est possible d'arriver très rapidement é des résultats satisfaisants, en utilisant un réseau, une librairie et du code déjé prèts é l&#8217;emploi.
        </p>
        
        <p>
        </p>
