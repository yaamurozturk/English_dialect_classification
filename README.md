# English dialect classification
This project focuses on the classification of the English language according to the chosen dialects. 
Project made for a course name I don't remember :d. All results and images are in the notebook file.
Made by me, Katia Kolos, Julie Nguyen and Oscar Moreno Escobar. 

Professor: Alice Missud

Résumé
---
Ce dossier porte toute son attention sur la classification de la langue anglaise selon les dialectes choisis. Afin de vérifier à quel point la machine est en capacité de reconnaître le dialecte correspondant, on décide de prendre en compte des traits lexicaux propres à chacun. La partie syntaxe n’a pas été retenue comme candidat suffisant en vue de la forte standardisation de la langue Anglaise comme langue universelle. Aussi, différentes méthodes de classification ont été retenues pour la complétion de ce projet. On garde 6 types de classifieurs capables d’apprendre à la machine. Une comparaison et une analyse de chacun des résultats ont été effectuées, ce qui nous permet de mieux comprendre les résultats obtenus pour la partie évaluation des performances.

Introduction
---
L’analyse de données est l’un des plus gros enjeux qu’il y ait depuis quelques années maintenant. Analyser les données dessert un grand nombre de domaines, allant de la satisfaction cliente à la traduction multilingue. L’une des finalités à l’analyse de données serait la classification automatique de données.  Pour ce faire, on utilise bien évidemment des algorithmes qui permettent leur traitement et qui donnent aussi un poids à la sémantique des données textuelles. Pour ce faire, il nous est disponible de traiter avec Word2Vec, Doc2Vec et différents types de classifieurs (SVM, RandomForest, Logistic Regression, etc.). Différentes façons de prendre en compte la sémantique nous ont été présentées afin de mener à bien la classification de données. Pour notre part, nous avons choisi de porter notre projet sur la classification de l’anglais selon sa région « parlé/écrite ». 
L’anglais est une langue parlée à l’échelle internationale, ce qui conduit cette langue à connaître des variations d’utilisation selon la région dans laquelle elle est pratiquée. Il est vrai que cette dernière est assez standardisée, cependant on observe des « features »  propres aux locuteurs natifs. Certaines variations sonores, un lexique différent et l'orthographe de certains mots diffèrent. L’anglais utilisé au Royaume-Uni peut donc se distinguer de l’anglais « états-unien », de l’anglais canadien ou encore australien, ou indien.
Ainsi, on cherche à classifier l’anglais selon un certain nombre de critères explicités plus bas, parmi quatre régions, à savoir : Royaume-Uni (UK dans notre projet), États-Unis (US), Canada (CA) et Australie (AUS). 
La complétion de ce devoir se fait à l’aide des différents articles scientifiques du domaine pour nous guider dans la méthodologie à suivre et/ou donner un angle d’approche approprié, des techniques et une réflexion afin de mener à bien notre projet.
Il sera donc explicité les parties suivantes, à travers cinq grands axes de lecture :
- Collecte des données, nettoyage 
- Dictionnaire, traits particuliers :
- Traitement avec Word2vec, Doc2vec 
- Classifieur : Binary and multiclass
- Evaluation et Analyse
- Conclusion et perspective

1) Corpus
Constitution du corpus : récolte des données
Notre corpus se constitue de tweets récoltés par l’API de Twitter. Afin de récolter les tweets, chacun des membres du groupe a fait une demande d’accès en tant que compte administrateur / Développeur. Une fois s’être inscrit et avoir rempli les formulaires et condition d’utilisation propre à l’API Twitter, différentes clés sont fournies afin de scrapper le contenu du réseau en question. Il faudra donc prendre garde à bien les conserver pour pouvoir les utiliser et scrapper avec le code en question.

Une fois l’accès autorisé, le scrapping commence. Chacun des dialectes représente dans notre projet les classes. Pour chacune des classes, une liste de « users » a été déterminé afin de cibler la récolte sur des tweets spécifiques.
On définit par « région » une liste de natif de la langue provenant de cette région anglophone. C’est environ une vingtaine de « users » qui a été sélectionné puis scrappé. On cherche à cibler des célébrités représentatives.  On trouvera donc une liste composé, respectivement de célébrité comme :
*UK : Emma Watson - US : Halsey - CA : Shawn Mendes - AUS : Alex Greenwich (et d’autres bien sûr)

A noter que différents types de célébrités ont été retenus pour le scrapping :
On retrouvera des agents propres au monde politique, du sport, célébrité (qui regroupe le mannequinat, le chant, la danse, acteurs)  et enfin, le monde journalistique.
C’est un total de 176 535 tweets qui ont pu être récupérés. Une partie sert pour l’apprentissage de la machine, et le reste comme test. 
Nota Bene : Une première approche fut de prendre en compte les #locations. Ceci était un moyen de cibler sur nos dialectes et donc d’avoir un premier tag de ce que nous cherchions. Cette idée fut vite laissé de côté puisque les #location sont un nombre moindre. La récolte serait donc pauvre et inintéressante en vue de l’objectif visé. Aussi, le lieu indiqué par le hashtag peut tout aussi bien signifier le lieu auquel le tweet a été écrit, ou encore le lieu où réside actuellement le user qui a tweeté. Avec un tel risque, il nous a semblé plus juste de choisir manuellement un nombre défini de personnes représentatives du dialecte. 

Nettoyage, et script utilisé
---
Le corpus étant composé de tweets, cela implique une étape crucial dans la réalisation du projet : le nettoyage de celui-ci. Les tweets présentaient essentiellement beaucoup d’hyperliens, de majuscules, caractères spéciaux, mais aussi des emojis.
On remarque aussi que la récolte de tweets nous amène à scrapper des tweets courts, non pertinents pour l’apprentissage de notre machine via un pipeline. Certains critères ont donc été avancés afin d’améliorer la qualité de notre corpus. On décide de ne pas prendre en compte les retweets, afin de garder les écrits originaux. D’ailleurs, les tweets courts (en dessous de 3 mots) ne sont pas comptabilisés.

2) Méthodologie
- Les étapes avant classifieurs
Comme dit précédemment, le but de ce devoir est de classifier un tweet selon une langue et ses quatre dialectes. Pour ce faire, on utilise des classifieurs sur python, afin d’effectuer cette tâche. Le corpus étant maintenant disponible, on décide de lancer un premier classifieur afin de voir comment ce dernier réagit à nos données.
C’est le classi
fieur Naives Bayes et CNN qui ont d’abord été choisis. Etrangement, CNN ne donne pas de résultat, et Naive Bayes nous donne des taux relativement bas. L’une de nos premières intuitions sur les résultats était dû au fait que les mots sont justement pris en tant que tel, comme dans un sac de mots, où chacun n’est pas pris selon son contexte mais de façon verbatim. On se dit donc que le contexte devait forcément être pris en compte pour de meilleurs résultats.
Un autre point crucial auquel nous avons pensé : il serait sûrement nécessaire de poser un « poids » sur certains mots selon leur appartenance. Autrement dit, il y aurait certains termes qui porteraient une pondération afin qu’ils puissent avoir une plus forte chance de tomber selon le terme et le dialecte associé à ce terme.
Ceci étant dit, il faut mettre en place un système de dictionnaire propre à chaque dialecte. Pour quelle raison ? L’anglais possède une richesse lexicale qui dépend de sa région. Certains termes ne s’emploient pas de la même façon et d’autres n'existent que dans un dialecte précis. On trouvera des variations orthographiques pour un même mot, un vocabulaire différent pour désigner un même sens, et d'autres particularités langagières propres à cette dernière.

Parmi les exemples que l’on peut citer, on remarque que l’anglais du Royaume Uni utilise le mot « cancelled » mais « canceled » en anglais états-unien. On pourrait aussi penser à toutes les variations possibles pour désigner les « toilettes » : ‘toilets’ (UK), ‘Restroom’ (US), ‘Bathroom’ (CA), ‘Washroom’ (AUS).
Ainsi, l’idée est la suivante : on décide de définir ‘toilets’ comme faisant partie du dictionnaire de UK. De la sorte, si ‘toilets’ apparaît dans le corpus, il aura un poids plus conséquent que les autres termes avoisinants, et sera « d’emblée » associé à la classe UK. On répète cette opération sur tous les termes propres à la classe UK, et faisons de même avec les autres classes et leurs lexiques spécifiques.

Finalement, nous préférons garder deux dictionnaires propres à deux classes, celui de la classe UK et la classe US. Nous décidons de laisser de côté les dictionnaires de la classe Canada et Australie. Le problème étant que ces dernières n’ont pas un dictionnaire aussi fourni comparé à la classe UK et US. Il ne nous semblait pas intéressant d’avoir des dictionnaires déséquilibrés en termes de nombres. On espère que la pondération ajoutée pour les mots propres aux classes UK et US prendront plus de poids afin d’être identifiée et si non, qu’ils seront soit dans la classe CA, soit AUS.

Aussi, peut-on ajouter que nous avions eu une intuition sur le fait de garder ou non les émojis. Pour quelles raisons ? Décider de garder les emojis au sein des tweets, se fait pour la simple et bonne raison que nous pourrions certainement déterminer si un emoji était privilégié dans un dialecte plutôt qu’un autre. Prenons comme exemple l’émoji qui suit : 🙏🏻

Pour la plupart des pays, cet émoji a pour trait de correspondre à l’innocence, parfois avec ironie certes mais, il peut aussi être compris comme une prière, ou bien représenter une bénédiction. Ceci est notamment visible aux Etats-Unis et en Amérique Latine, où le 🙏🏻 représente « le fait de faire le bien autour de soi ». En Chine en revanche, celui-ci signifie la mort et peut être perçu comme une menace voilée. 

(cf. : <https://www.google.com/amp/s/www.feminactu.com/2020/07/attention-la-signification-des-emojis-peut-varier-dun-pays-a-un-autre/amp/>)

On prend donc en compte les dictionnaires et considérons dans un premier temps la suppression des émojis mais aussi un essai en leur présence dans notre corpus. Et pour avoir une meilleure visibilité de ce qu’il se passe, c’est avec plusieurs classifieurs que l’on soumet notre corpus. Une bonne approche serait le processus suivant :
Notre corpus sert de base d’apprentissage à la machine afin que le classifieur sache ce qu’il faut apprendre et/ou relever. Pour se faire, on divise pour chacun des classifieurs les données de notre corpus en deux parties : une première partie à 60% et une deuxième partie à 40%. La partie à 60% sera utilisée comme apprentissage et les 40%, seront pour le test. 

Enfin, on soumet les différentes parties des données au classifieur et une fois qu’il est soumis, nous utilisons des métriques afin d’évaluer les performances du classifieur. On affichera les mesures de rappels, de précision et de recall en plus de matrices de confusion.

Il ne faut pas oublier qu’afin d’avoir une classification qui prend en compte le sens d’un mot, il faut lui donner une représentation vectorielle et commencer par de la classification binaire entre toutes nos classes. Cela permet d’avoir une première idée de ce qu’il se passe.

- La représentation vectorielle des données

Les plongements lexicaux ont été obtenus à l’aide de la bibliothèque gensim. Nous avons décidé de faire 3 types de vecteurs : un Doc2Vec, un Word2Vec.  Quatre modèles ont été utilisés. D’un côté, un Doc2Vec et un Word2Vec avec la version lemmatisé du corpus puis un Doc2Vec et un Word2Vec du corpus sans lemmatisation.
Le Word2Vec mean renvoie un vecteur moyen de chaque tweet. Lors de l' obtention des plongements, certaines manipulations ont dû être effectuées sur le corpus. En effet, en enlevant la ponctuation, les stop words et les emojis, il en résultait des tweets vides. Il a été décidé de traiter cette erreur comme une exception à l’aide de l’instruction try…except dans notre code. Après ceci, on obtient les tweets qui comportent du contenu textuel.  

- Les Classifieurs

Pour les deux modèles de plongements lexicaux, nous avons fait des tests de classification binaire et multiclasse avec différents algorithmes de scikit-learn: kNN, SVM, Naive Bayes, Random Forest, Régression Logistique pour la classification binaire et kNN, SVM, Random Forest, Régression Logistique pour la classification multiclasse. 
Ce dossier présentera par la suite chacun des modèles utilisés. Il sera explicité le schéma de code utilisé pour utiliser les classifieurs, le modèle train et la partie test, et enfin les résultats de la performance de nos classifieurs. On trouvera aussi le fonctionnement des résultats obtenus selon le classifieur. On tente d’expliquer la raison de ces résultats selon l’algorithme de chacun.

SVM
---
Le SVM est une technique d'apprentissage automatique qui trouve la meilleure séparation possible entre les classes. Le SVM trouve l'hyperplan qui maximise la marge de séparation entre les classes. Ces hyperplans sont appelés des kernels.
Les Kernels fonctionnent comme des fonctions qui transforment un espace de faible dimension en un espace de plus grande dimension. En d’autres termes, ces fonctions quantifient la similarité entre deux observations dans un nouvel espace dimensionnel. Le modèle SVM admet plusieurs types de Kernels, nous avons limité nos essais à deux types : polynomial et linéaire.

Nous avons donc testé la classification à l’aide de deux kernels différents, Il s’est avéré qu’en utilisant le premier la classification prenait trop de temps (2 à 3 fois plus de temps que le linéaire). Certes, les résultats étaient légèrement meilleurs avec le polynomiale mais pas assez pour justifier le temps écoulé pendant la classification. Il a été décidé de ne pas seulement faire la classification SVM linéaire.
Les résultats les plus parlant pour cet algorithme correspondent à la classification US-UK (70%)  même si la différence entre la moyenne de l'exactitude tous algorithmes confondus (65%) n’est pas énorme, on peut toutefois affirmer que c’est notre meilleur résultat de classification binaire.
Il est bien possible que l’utilisation des dictionnaires ait influé sur ce résultat. Cependant, on a repéré un phénomène dans la classification binaire et c’est qu’une des deux classes est mieux classée que l’autre.Il a été rare de voir que les résultats étaient presque équilibrés entre deux classes. Cela pourrait être dû à la nature de la tâche. En effet, s’agissant de deux dialectes de la même langue leurs similitudes sont plus saillantes que leur différences ce qui va mettre en difficulté l’algorithme pour bien tracer la frontière entre les classes.  


K Nearest Neighbors
---
Ce classifieur est le moins performant sur l’ensemble de nos tests, que ce soit la classification binaire ou multiclasse : presque avec toutes les représentations vectorielles et presque toutes les paires de dialectes, son accuracy est inférieure à celles de la régression logistique, SVM (même LinearSVC) et random forest. 
Nous pouvons pourtant remarquer que dans la classification multiclasse, ce classifieur fait des prédictions plus équilibrées (si on compare le nombre de prédictions correctes) entre les dialectes que les autres classifieurs. C’est le seul classifieur qui sait distinguer ‘UK’ dans le cas de la classification multiclasse. Voici une idée des matrices de confusion obtenus, à comparer pour la représentation de mean word2vec lemmatisé et non : 
- RandomForestClassifier
- LogisticRegression
- KNeighborsClassifier
- LinearSVC

Logistic Regression
---
On tente aussi de donner notre dataset au classifieur de Logistic Regression. Bien sûr, ce classifieur, comme tous les autres classifieurs, est sollicité pour le machine learning et notamment pour la classification selon 3 types :
- la classification binaire (binomial)
- la classification multiclasse (multinomiale)
- la classification d’ordre (ordinale)
Dans notre cas, on applique ce classifieur pour une première classification binaire. Ainsi, on tente de comparer certaines classes entre elles, et entre classifieurs. On décide donc de comparer comme avec les autres classifieur les classes UK vs US. Les résultats nous donneront un aperçu de ce qui marche le mieux ou non entre classifieur, pour les mêmes classes sous étude. 

Pour la classification binaire entre les classe UK vs US, on voit que l’accuracy est de 0.67 (soit 67,7%). Ce qui n’est pas trop mal pour une première lancée. Toutefois, cela reste loin d’être satisfaisant. 
D’autres combinaisons de langues ont été effectuées mais les résultats nous paraissent biaisés pour de drôle de raison. C’est en effet toujours la classe Australia qui était le mieux reconnue sachant que la classe AUS n’avait pas de dictionnaire à son bord puisque trop pauvre, et cette dernière a légèrement moins de données que les autres classes. Comparé aux autres classifieurs, Logistic Regression n’est pas le meilleur mais pas le pire non plus. En binaire, ce n’est pas une catastrophe puisque l’étiquette Y aura deux valeurs possibles 0 ou 1, soit Anglais = {0, 1}, respectivement 0 = UK et 1 = US. Dans ce cas de figure, c’est un peu comme le “pendant” de la Régression Linéaire qui est repris, où l’on a que deux valeurs possibles (0 ou 1).

La classification de l’anglais, en prenant compte de la fonction score, se fait donc dans cette logique ci (pour une classification binaire) :
- Cas 1)  Input > 0 , quand la classe (étiquette) vaut 1
- Cas 2) Input < 0, quand la classe (étiquette) vaut 0
La fonction score qu’on a obtenue intègre les différentes variables prédictives. A cette fonction, on appliquera la fonction sigmoid (Sigmoid Function). Cette fonction produit des valeurs comprises entre 0 et 1. D’après nos résultats, c’est la classe UK qui est le mieux prédit dans notre cas. 
Etrangement, les résultats sont meilleurs quand il n’y a pas de lemmatisation des données. Il faut maintenant voir comment la classification s’opère pour du multiclasse.
On prend en compte cette fois-ci toutes nos classes, et on étend nos classifieurs à du multiclass classification. On obtient donc les résultats ci-dessous :

En multiclasse, les résultats sont très bas, pour ne pas dire plutôt mauvais. Logistic Regression n’offre pas de bonne performance et cela est sans surprise puisque la réflexion qui se cache derrière est celle-ci :
-Étape 1 : On considère que l’anglais UK est  la classe positive (étiquette 1) et le reste comme la classe négative (dans ce cas, US, AUS et CA seront dans le même groupe de classe négative (étiquette 0) ), et on entraîne la régression logistique sur cette configuration de données. Ce qui  produira une fonction de prédiction 
-Etape 2 : On considère l’anglais US comme la classe positive et le reste comme la classe négative, et on entraîne la régression logistique pour obtenir une deuxième fonction de prédiction : 
-Etape 3 : On considère l’anglais CA comme la classe positive et le reste comme la classe négative, et on entraîne la régression logistique
De même, on considère l’anglais AUS comme positif et le reste comme négatif, et on entraîne la régression logistique dessus.
Toutes ces étapes nous permettent d’établir une probabilité que x input va être d’une classe Y. La bonne classe de l’observation x est celle pour laquelle on a la plus grande probabilité. 

Random Forest 
---
Le classifieur Random Forest utilise des arbres de décision et fonctionne par méthodes symboliques cherchant à classer les données de celles qui sont les plus informatives ou les plus discriminantes pour ensuite évaluer celles qui sont les moins différentes dans notre corpus.
Pour trouver les éléments les plus discriminants, l'algorithme évalue la différence ou l'homogénéité d'une donnée en calculant la fonction Gini. Cette évaluation se fait également en utilisant des seuils dans le cas où un attribut ou une caractéristique parmi nos données n'est pas définitif pour classer notre corpus.
Scikit learn nous permet d'utiliser l'algorithme avec certains paramètres pour mieux répondre à notre tâche de classification. Les principaux paramètres à ajuster lors de son utilisation sont «n_estimators» et « max_features » . Le premier est le nombre d'arbres dans la forêt. Normalement, plus il y a d'arbres, meilleure est la classification, mais plus le calcul est long. « n_estimators » est la taille des sous-ensembles aléatoires de caractéristiques à considérer lors de la division d'un nœud.
Nous avons tout d'abord testé avec une profondeur maximale de 5 avec 300 estimateurs, ce qui n'a pas donné des résultats idéaux pour la classification multi-classe.  Nous avons pensé que cela pouvait être dû à un certain déséquilibre dans notre corpus. 
Selon la documentation de Scikit learn, les bonnes valeurs empiriques par défaut sont « max_features= sqrt » pour les tâches de classification (où nombre des features est le nombre de caractéristiques dans les données). De bons résultats sont souvent obtenus en définissant «  max_depth=None  » en combinaison avec « min_samples_split=2 » . Nous avons également essayé ces paramètres en fonction des consignes. Les valeurs par défaut donnent en effet de meilleurs résultats que des paramètres différents, notamment pour la classification binaire.
Dans la comparaison finale de tous les classifieurs, nous avons choisi les paramètres par défaut de Random Forest.
En bref…

Conclusion et Perspective
---
Ce projet nous a permis de donner une première base de la classification de dialecte qui peut être reprise pour d’autres langues et ses dialectes. Cette base se compose d'une méthodologie simple mais exploratoire en termes d’hypothèses. On reprend bien sûr le prétraitement, essentiel au bon traitement de notre corpus. Le nettoyage du corpus, qui comprend donc la suppression des stop words, les emojis, on essaie aussi la lemmatisation ou non, ce qui permet de voir les performances de nos classifieurs selon des données lemmatisées ou non lemmatisées. Par la suite, on lance les classifieurs selon une classification binaire ou multiclasse, parmi les algorithmes suivants : SVM, KNN, Logistic Regression, Random Forest. Les performances de chacun d’entre eux sont plus ou moins équivalentes mais c’est SVM qui a les meilleurs résultats malgré un temps de traitement extrêmement long. 

D’autres options de prétraitement ont été envisagées et faites. On pourra notamment citer la lemmatisation de nos données avec Word2Vec et Doc2Vec, en plus des emojis gardés. Malheureusement les emojis n’ont pas d’impact suffisant pour jouer un rôle dans la meilleure classification des données. Notre hypothèse d’origine n’est donc pas validée.

En revanche, il est vrai que d’autres possibilités pourraient être ajoutées à notre devoir pour la meilleure classification de dialectes. On pense notamment à la prise en compte de l’oral comme point d’appuie et qui aiderait grandement à la classification. Bien sûr, cela engendre évidemment des temps de récoltes du corpus plus conséquent, puisque les données issues de l’oral ne sont pas des plus propres. Prendre en compte la prosodie, le rythme, la phonologie de chaque dialecte auraient pu être un poids dans le choix des classes pour une donnée.

Un autre point à envisager serait de prendre en compte des mots spécifiques comme les link words - ou autre catégorie de mot comme les modaux et semi-modaux - et de regarder la répartition de chacun d’entre eux. Le but étant de voir si un dialecte tend à plus utiliser des linkwords que d'autres, et ainsi émettre un poids pour ces derniers. Une étude statistique grâce aux techniques de linguistique de corpus et le langage R nous permettent de visualiser ceci. Cela pourrait être un autre appuie à des fins de classifications.

Enfin, la tâche fut un peu difficile en vue de notre choix de sujet et du corpus dont nous avions disposé, mais elle fut enrichissante et pourrait être poursuivie avec les suggestions que nous avons citées plus haut. Le dossier a été complété et nos hypothèses et intuitions vérifiées, parfois confirmées, parfois non, mais c’était un plaisir de le faire. On finira avec la conclusion suivante : l’australien se distingue le plus de l’anglais US qui lui-même se distingue de l’anglais britannique. En revanche, l’anglais US est très proche de l’anglais canadien.
