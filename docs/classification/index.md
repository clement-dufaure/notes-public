<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

# TD Clustering

# Exercice 1 : K Means

## 1-1 Différents paramétrages

| 1 | 2 | 9 | 12 | 20 |

---

a) $K=2;μ_1=1;μ_2=7$

K nombre de classe

Dans K-means, **le nombre de classe est un paramètre**, il est défini a priori

On choisit alors au hasard autant de points que de classes (notés $µ_i$), ce sont les barycentres des classes à l'itération 0.

### Itération 1

| 1 | 2 || 9 | 12 | 20 |
|-|-|-|-|-|-|
| x |  |x|  | |  |
| $µ_1=1$ |  |$µ_2=7$|  | |  |

- Points plus proche de $µ_1$ que de $µ_2$ : 1,2

- Points plus proche de $µ_2$ que de $µ_1$ : 9,12,20

Classes à l'itération 1 : 

| 1  2 || 9  12  20 |

Barycentre de ces classes :
- Classe 1 : $(1+2)/2=1.5$
- Classe 2 : $(9+12+20)/3=13.7$

### Itération 2

| 1 || 2 | 9 | 12 || 20 |
|-|-|-|-|-|-|-|
|| x |  ||  |x |  |
|| $µ_1=1.5$ |  ||  |$µ_2=13.7$ |  |

- Points plus proche de $µ_1$ que de $µ_2$ : 1,2

- Points plus proche de $µ_2$ que de $µ_1$ : 9,12,20

Les classes sont stables : 

| 1  2 || 9  12  20 |

Fin de l'algorithme

---

b) $K=2;μ_1=1;μ_2=20$

### Itération 1

| 1 | 2 | 9 | 12 | 20 |
|-|-|-|-|-|-|-|
|x||||x ||
|$µ_1=1$||||$µ_2=20$||

- Points plus proche de $µ_1$ que de $µ_2$ : 1,2,9

- Points plus proche de $µ_2$ que de $µ_1$ : 12,30

Classes à l'itération 1 : 

| 1  2 9 || 12  20 |

Barycentre de ces classes :
- Classe 1 : $(1+2+9)/3=4$
- Classe 2 : $(12+20)/2=16$

### Itération 2

| 1 | 2 || 9 | 12 || 20 |
|-|-|-|-|-|-|-|
|||x|||x||
|||$µ_1=4$|||$µ_2=16$||

- Points plus proche de $µ_1$ que de $µ_2$ : 1,2,9

- Points plus proche de $µ_2$ que de $µ_1$ : 12,30

Les classes sont stables : 

| 1  2 9 || 12  20 |

Fin de l'algorithme

---

Remarque : pour 2 tirages, on a obtenu deux classifications différentes

=> Existance d'optimum locaux

---

c)$K= 3,μ1= 1,μ2= 12 ,μ3= 20$

### Itération 1

| 1 | 2 | 9 | 12 | 20 |
|-|-|-|-|-|-|-|
|x|||x|x ||
|$µ_1=1$|||$µ_2=12$|$µ_3=20$||

- Points plus proche de $µ_1$ : 1,2
- Points plus proche de $µ_2$ : 9,12
- Points plus proche de $µ_3$ : 20

Classes à l'itération 1 : 

| 1  2 || 9 12 || 20 |

Barycentre de ces classes :
- Classe 1 : $0.5$
- Classe 2 : $10.5$
- Classe 2 : $20$

Classes stables

---

d)$K= 4,μ1= 1,μ2= 9,μ3= 12 ,μ4= 20$

### Itération 1

| 1 | 2 | 9 | 12 | 20 |
|-|-|-|-|-|-|-|
|x||x|x|x ||
|$µ_1=1$||$µ_2=9$|$µ_3=12$|$µ_4=20$||

- Points plus proche de $µ_1$ : 1,2
- Points plus proche de $µ_2$ : 9
- Points plus proche de $µ_3$ : 12
- Points plus proche de $µ_4$ : 20


Classes stables

## 1-2 Un critère de sélection

On veut :
- Classes homogènes (= Inertie intra faible)
- Classes différentes entre elles (= Inertie inter forte)

Inertie totale = Inertie intra + Inertie inter

Pour une classe $k$, $I_{INTRA_k}=\sum_{i\in k}p_id²(x_i,G_k)$

Avec :
- $i\in k$ les éléments i de la classe k
- $G_k$ le barycentre de la classe k
- $d$ une distance à définir (paramètre de la méthode)
- $p_i$ les poids relatifs au sein de la classe ($\sum_ip_i=1$ en sommant sur les individus de la classe). En l'absence d'indications, les individus sont équipondérés.

Au total, on pondère par les effectifs des classes :

$I_{INTRA} = \sum_{k=1}^K\frac{n_k}{n}I_{INTRA_k}$

Soit pour les classifications précédentes :

a)

Classe {1 2} : Barycentre=0.5 $I_{INTRA}=1/2(0.5²+0.5²)=0.25$
Classe {9 12 20} : Barycentre=13.7 $I_{INTRA}=1/3(4.7²+1.7²+6.3²)=21.6$

Soit au total $I_{INTRA}=2/5*0.25+3/5*21.6=13.06$

b)

Classe {1 2 9} : Barycentre=4 $I_{INTRA}=1/3(3²+2²+5²)=12.67$
Classe {12 20} : Barycentre=16 $I_{INTRA}=1/2(4²+4²)=16$

Soit au total $I_{INTRA}=3/5*12.67+2/5*16=14$

Dans la classification obtenue avec b), les classes sont moins homogènes

c)

Classe {1 2} : Barycentre=0.5 $I_{INTRA}=1/2(0.5²+0.5²)=0.25$
Classe {9 12} : Barycentre=10.5 $I_{INTRA}=1/2(1.5²+1.5²)=2.25$
Classe {20} : Barycentre=20 $I_{INTRA}=0$

Soit au total $I_{INTRA}=2/5*0.25+2/5*2.25+1/5*0=1$

d)

$I_{INTRA}=0.1$

:warning: Ce critère n'a de sens que si on compare des classifications avec le même nombre de classe !!!
Avec plus de classe, on a FORCÉMENT moins d'inertie intra !
Sinon la meilleure classification est celle avec n classes singleton ($I_{INTRA}$ nulle !)

# Exercice 2 : CAH

## 2-1 Une première CAH à la main

Regrouper les individus en utilisant la *classification hiérarchique ascendante* et en prenant comme mesure de similarité *la distance euclidienne* et comme critère d’agrégation *le linkage single*.

3 paramètres
- la méthode CAH, qui implique deux paramètres
- la mesure de similarité ~ distance entre points
- le critère d'aggrégation ~ distance entre classes

Rappel : distance euclidienne entre x et y : $\sqrt{\sum_{j=1}^p(x_j-y_j)²}$ 

linkage single ? $d(Classe_1,Classe_2)=min_{x\in Classe_1,y\in Classe_2}d(x,y)$
En d'autres termes, le plus petite distance possible entre un point de chacune des classe.

algorithme de CAH ?
*classification* : ok
*hierarchique* : l'output de la méthode sera une hiérachie dans laquelle on va choisir une partition (ou classification)
*ascendante* : l'état initial de l'algorithme sera les singletons (5 classes de 1 employé)

### Itération 1

Classes : |E1|E2|E3|E4|E5|

Calcul des distances entre individus :

|Employé |E1|E2|E3|E4|E5|
|- |- |- |- |- |- |
|Ancienneté| 2| 3| 5| 6| 8|
|Salaire| 2000| 2100| 3500| 4100| 10000|



|  |E1|E2|E3|E4|E5|
|- |- |- |- |- |- |
|E1| 0|100|1500|2100|8000|
|E2|  | 0|1400|2000|7900|
|E3|  |  | 0|600|6500|
|E4|  |  |  | 0|5900|
|E5|  |  |  |  | 0|

(arrondies au centième 

Entre E1 et E2 par exemple : $d(E1,E2)=\sqrt{(2000-2100)²+(3-2)²}=\sqrt{100²+1²}=\sqrt{10001}\approx \sqrt{10000}$

Remarque : On retrouve quasiment la distance en ne considérant que la variable Salaire 

Les deux individus (classes singletons) les plus proches sont E1 et E2, on les regoupe

### Itération 2

Classes : |E1 E2|E3|E4|E5|

Disatances entre classe selon le critère du linkage single (distance minimale)

|  |E1 E2|E3|E4|E5|
|- |- |- |- |- |- |
|E1 E2| 0|1400|2000|7900|
|E3|    | 0|600|6500|
|E4|    |  | 0|5900|
|E5|    |  |  | 0|

Les deux classes les plus proches : singletons E3 et E4

### Itération 3


|  |E1 E2|E3 E4|E5|
|- |- |- |- |- |- |
|E1 E2| 0|1400|2000|7900|
|E3 E4|    | 0|6500|
|E5|    |  |  0|

Les deux classes les plus proches : {E1 E2} et  {E3 E4}

### Itération 4

|  |E1 E2 E3 E4|E5|
|- |- |- |- |- |- |
|E1 E2 E3 E4| 0|5900|
|E5|    |  0|

Forcément on regroupe les deux classes restantes et on obtient une classe avec tout le monde

 **Choisir une classification**
 
 La méthode ne donne pas une mais une succesion de classification plausible
 
Il faut savoir quand s'arrêter

Pas facile avec la méthode linkage simple, souvent on utilise le critère de Ward. La distance entre classe est alors le regroupe ment qui fait perdre le moins d'inertie intra.

Avec le critère de Ward, on peut prendre en compte la "vitesse" de gain d'inertie intra lors d'un regroupement

Remarque : sous R, en utilisant FactoMineR (qui utilise lui même agnes), on peut choisir comme méthode :
```
 method: character string defining the clustering method.  The six
          methods implemented are '"average"' ([unweighted pair-]group
          [arithMetic] average method, aka 'UPGMA'), '"single"' (single
          linkage), '"complete"' (complete linkage), '"ward"' (Ward's
          method), '"weighted"' (weighted average linkage, aka
          'WPGMA'), its generalization '"flexible"' which uses (a
          constant version of) the Lance-Williams formula and the
          'par.method' argument, and '"gaverage"' a generalized
          '"average"' aka "flexible UPGMA" method also using the
          Lance-Williams formula and 'par.method'.
```



## 2-2 2-3 *Valeurs standardisées* 

Standardiser (réduire) ? un souvenir des différences entre ACP normées ou non ?

```
      anciennete     salaire
[1,] -1.17279094 -0.71128234
[2,] -0.75393703 -0.68088566
[3,]  0.08377078 -0.25533212
[4,]  0.50262469 -0.07295204
[5,]  1.34033251  1.72045216
```

Disparition des problèmes d'ordre de grandeur entre les variables ancienneté et salaire.
Même problématique que l'ACP normée : résoudre les problèmes d'unité, de dimension,...

- nouvelles distances

```
     [,1] [,2] [,3] [,4] [,5]
[1,]    0 0.42 1.34 1.79 3.50
[2,]    0 0.00 0.94 1.40 3.19
[3,]    0 0.00 0.00 0.46 2.34
[4,]    0 0.00 0.00 0.00 1.98
[5,]    0 0.00 0.00 0.00 0.00
```


---

Compléments

- ACP + CAH : on effectue une ACP, on utilise un critère de sélection d'axe, et on effectue la CAH sur les données nettoyées"
```r
# Pour ne conserver que les 3 premiers axes
res.PCA<-PCA(data,scale.unit=TRUE,graph=FALSE,ncp=3)
# CAH qui utilise uniquement les 3 premiers axes factoriels 
res.HCPC=HCPC(res.PCA)
```


- Variables qualitatives ? : on effectue une ACM (on sélectionne les axes) et la CAH se fait sur les axes factoriels
```r
# Pour ne conserver que les 3 premiers axes
res.MCA<-MCA(data,scale.unit=TRUE,graph=FALSE,ncp=3)
# CAH qui utilise uniquement les 3 premiers axes factoriels de l'ACM 
res.HCPC=HCPC(res.MCA)
```




# Exercice 3 : Mélanges

## Préambule

- Qu'est ce qu'un "mélange" de lois ?

On considère un échantillon $x= (x1,...,xn)$ composé de $n$ observations indépendantes $x_i∈X$. Chaque observation est issue d’un mélange à $K$ composantes déterminées par $p(x_i;θ)=\sum_{k=1}^{K}π_kp_k(x_i;α_k)$,avec$θ∈Θ$.

![](https://i.imgur.com/My5TbxD.png)
=> loi inconnue compliquée à décrire, à paramétrer


![](https://i.imgur.com/FUWKgUo.png)
=> 2 lois normales superposées

Idée : 
- chaque point a une probabilité $\pi_k$ d'appartenir à une des deux courbes (= proportion des points correspondant à chacune des 2 courbes, bien entendue inconnue), $\sum \pi_k =1$
- la loi de chaque courbe est $p_k(x_i;α_k)$ avec $α_k$ les paramètres de la loi $p_k$ (si $p_k$ est une loi normale $\alpha_k=(\mu_k,\sigma_k)$)
- Ce qui donne en additionnant chaque loi probable $p(x_i;θ)=\sum_{k=1}^{K}π_kp_k(x_i;α_k)$

a)
- log-vraisemblance $l(θ;x)$

Vraissemblance : $L(\theta,x)=\prod_{i=1}^np(x_i;θ)$

$l(θ;x)$ = $\sum_{i=1}^{n}ln(p(x_i;θ))$
         = $\sum_{i=1}^{n}ln(\sum_{k=1}^{K}π_kp_k(x_i;α_k))$
         
On obtient une équation sous une forme difficilement estimable (même par optimisation par un logiciel)


- log-vraisemblance complétée $l(θ;x,z)$

Idée : si on sait à quelle classe appartient chaque point, la loi est beaucoup plus simple

On introduit la variable catégorielle de l'appartenance à la classe : $Classe_i=k$
Pour rester numérique on choisit de la noter avec des variables booléenne $Z_k$, telle que $z_{i,k}=1$ si $Classe_i=k$, sinon $z_{i,k}=0$

Pour le point $i$, $p(x_i;θ \cap Classe_i=k)=p(Classe_i=k)p(x_i;\theta|Classe_i=k)$
$=p(z_{i_k}=1)p_k(x_i;α_k)=\pi_kp_k(x_i;α_k)$

La "contribution" à la log-vraissembalnce du point $i$ appartenant à la classe k_0 est donc :
$$
ln(\pi_{k_0}p_{k_0}(x_i;α_{k_0}))=z_{i_{k_0}}ln(\pi_{k_0}p_{k_0}(x_i;α_{k_0}))
$$
car $z_{i_{k_0}}=1$
$$
=\sum_{k=1}^{K}z_{i,k}ln(π_kp_k(x_i;α_k))
$$
car $z_{i_{k}}=0, \forall k\neq k_0$

soit

$l(θ;x,z)=\sum_{i=1}^{n}\sum_{k=1}^{K}z_{i,k}ln(π_kp_k(x_i;α_k))$

le modèle reste complexe, mais peut être résolu par l'algorithme EM qui va avoir le bon gout de nous donner une estimation des $Z_k$ (et donc une classification)

b)

$t_{i,k}(θ)$ probabilité *a posteriori* sous le paramètre $\theta$  que  l’observation $i$ soit  issue de la composante $k$.
:warning: les $\pi_k$ sont les probabilité *a priori* et **font partie** de $\theta$ !!!

Calcul de probabilité à posteriori (Bayes)
$$
t_{i,k}(θ)=P_\theta(z_{i,k}=1|X_i=x_i)=\frac{P_\theta(z_{i,k}=1)P_\theta(X_i=x_i|z_{i,k}=1)}{P_\theta(X_i=x_i)}
=\frac{\pi_kp_k(x_i;\alpha_k)}{p(x_i;\theta)}
$$

=> $t_{i,k}$ est donc l'espérance conditionnelle de $z_{i,k}$ sachant $x_i$ (espérance d'un Bernoulli B = P(B=1))

=> pour un i donné, la meilleure espérance parmi les k nous donne la classe la plus probable. Donc non seulement on va obtenir une classification, mais en plus on sera capable de mesurer à quel point un point est vraiment sûr dans une classe ou en ballotage (cas avec des probas 0.9/0.1 VS probas 0.49/0.51)



c)

Soit $E(t(θ),z)=−\sum_{i=1}^{n}\sum_{k=1}^Kz_{i,k}ln(t_{i,k}(θ))$, 
avec $t(θ) = (t_{i,k}(θ);i= 1,...,n;k= 1,...,K)$ (vecteur des probabilités a posteriori)

Vérifier la formule d’Hathaway :
$l(θ;x) =l(θ;x,z) +E(t(θ),z)$

À partir du calcul de $t_{i_k}$ précédent, que l'on passe au logarithme :
$ln(t_{i,k}(θ))=ln(\pi_kp_k(x_i;\alpha_k))-ln(p(x_i;\theta))$
$$
\implies \sum_{k=1}^Kz_{ik}ln(t_{i,k}(θ))=\sum_{k=1}^Kz_{ik}ln(\pi_kp_k(x_i;\alpha_k))-ln(p(x_i;\theta))
$$
On n'a pas "passé à la somme" l'équation,
on utilise simplement le fait que :
$$
ln(t_{i,k}(θ))=\sum_{k=1}^Kz_{ik}ln(t_{i,k}(θ)) \text{ et } ln(\pi_kp_k(x_i;\alpha_k))=\sum_{k=1}^Kz_{ik}ln(\pi_kp_k(x_i;\alpha_k))
$$
car $z_{ik}$ vaut 1 pour le "vrai" k, 0 pour les autres, on rajoute donc des zéros
$\iff ln(p(x_i;\theta)) = \sum_{k=1}^Kz_{i,k}ln(\pi_kp_k(x_i;\alpha_k)) - \sum_{k=1}^Kz_{i,k}ln(t_{i,k}(θ))$


Soit en sommant sur i :
$l(\theta;x) = l(\theta,x,z) + E(t(θ),z)$



## L'algorithme EM

EM = espérance - maximisation

Paramétrage "fixe" : le nombre de classe K

Initialisation : choix d'un paramètre $\theta^{[0]}$ : $\theta$ est constitué des $\pi_k$ + des vecteurs $\alpha_k$ de chaque loi constituant le mélange
Exemple : mélange de 3 lois normales : 9 paramètres, les 3 proportions de classes + la moyenne et la variance de chaque classe (en réalité 8 paramètres car la dernière proportion est contrainte par 100-les deux premières)

Sur une itération $r$
- l'étape d'espérance : calcul de la logvraissamblance complété passant par le calcul des $t_{i_k}(\theta^{[r-1]})$
En effet la log vraissemblance complété vaut
$l(θ;x,z)=\sum_{i=1}^{n}\sum_{k=1}^{K}z_{i,k}ln(π_kp_k(x_i;α_k))$, comme on ne connait pas Z, on remplace par son espérance qui est donc $t_{i_k}$

- l'étape de maximisation : on maximise l'espérance de la vraissamblance complétée, c'est à dire recherche du nouveau $\theta^{[r]}$ qui maximise $\sum_i\sum_kt_{i,k}(\theta^{[r-1]})ln(\pi_kp_k(x_i;\alpha_k))$


On itère jusqu'à stabilisation de la vraissemblance

:warning: initialisation aléatoire => possibilité de tomber sur un maximum local => lancer l'algorithme pusieurs fois et conserver le meilleur résultat

## Convergence de l'algorithme

$Θ$ est l'espace des paramètres possibles

Soit $\tilde θ∈Θ,θ∈Θ$, montrer que 
$$
l(θ;x)=Q(θ;\tilde \theta)−H( \theta;\tilde \theta)
$$
avec 
$$
Q(θ;\tilde \theta) =E_{\tilde \theta}[l(θ;x,z)|X_i=x_i]
$$
**Attention, erreur d'énoncé :**
$$
H(θ;\tilde \theta) =\sum_{i=1}^n\sum_{k=1}^nE_{\tilde \theta}[z_{i,k}ln(t_{ik}(\theta))|X_i=x_i]
$$
et $E_{\tilde θ}[·]$ l'espérance prise en considérant la distribution mélange avec le paramère $\tilde θ$.

Rappel : à chaque étape on cherche à maximiser un paramètre $\theta$ en se servant de la valeur qu'il avait à l'itération prédédente pour calculer la vraissamblance complétée.
dans les écritures de $H$ et $Q$, $\tilde \theta$ est le paramètre de l'itération précédente, $\theta$ est le nouveau paramètre à rechercher pour maximiser la vraissemblance.


$$
l(θ;x)=\sum_{i=1}^n ln(p(xi;\theta))= \sum_{i=1}^n\sum_{k=1}^Kz_{i,k}ln(\pi_kp_k(x_i;\alpha_k)) - \sum_{i=1}^n\sum_{k=1}^Kz_{i,k}ln(t_{i,k}(θ))
$$
(Voir formule d'Hathaway plus haut)

On passe à l'espérance sous le paramètre $\tilde \theta$ conditionnellement à $X_i=x_i$
La seule chose aléatoire, ce sont les $z_{i,k}$, qui vont dont être estimés par leur espérance qui se calcule dans le cadre d'un paramétrage, ici celui de l'itération précédente $\tilde \theta$
$$
\sum_{i=1}^n E_{\tilde \theta}[ln(p(xi;\theta))|X_i=x_i]= \sum_{i=1}^n\sum_{k=1}^KE_{\tilde \theta}[z_{i,k}ln(\pi_kp_k(x_i;\alpha_k))|X_i=x_i] - \sum_{i=1}^n\sum_{k=1}^KE_{\tilde \theta}[z_{i,k}ln(t_{i,k}(θ))|X_i=x_i]
$$
le premier terme est déterministe, il s'agit de l'espérance d'un scalaire
$$
\iff \sum_{i=1}^n ln(p(xi;\theta)) = \sum_{i=1}^n\sum_{k=1}^KE_{\tilde \theta}[z_{i,k}ln(\pi_kp_k(x_i;\alpha_k))|X_i=x_i] - \sum_{i=1}^n\sum_{k=1}^KE_{\tilde \theta}[z_{i,k}ln(t_{i,k}(θ))|X_i=x_i]
$$
on resimplifie ensuite les expressions de log vraissemblance et log vraissemblance complétée pour revenir à la formule
$$
\iff l(\theta;x) = E_{\tilde \theta}[l(\theta;x,z)|X_i=x_i] - \sum_{i=1}^n\sum_{k=1}^KE_{\tilde \theta}[z_{i,k}ln(t_{i,k}(θ))|X_i=x_i]
$$
$$
\iff  l(\theta;x) = Q(\theta,\tilde \theta) - H(\theta,\tilde \theta)
$$

La formule est vraie quelquesoit $\theta$ est quelquesoit $\tilde \theta$

*Écrire la différence entre les log-vraisemblances obtenues aux itérations $r$ et $r−1$ à partir des fonctions Q et H*

On va utiliser la formule deux fois :
- une fois avec $\theta = \theta^{[r]}$ et $\tilde \theta = \theta^{[r -1]}$
- une fois avec $\theta = \tilde \theta = \theta^{[r-1]}$

$$
l(\theta^{[r]};x)-l(\theta^{[r-1]};x)=Q(\theta^{[r]},\theta^{[r-1]}) -Q(\theta^{[r-1]},\theta^{[r-1]}) - H(\theta^{[r]},\theta^{[r-1]}) + H(\theta^{[r-1]},\theta^{[r-1]})
$$

On s'intéresse donc à l'évolution de la vraissemblance entre l'ancienne valeur (itération précédente) $\theta^{[r-1]}$ et la nouvelle valeur $\theta^{[r]}$, pour cela on le décompose sous le paramétrage de l'itération précédente fixé $\theta^{[r-1]}$ 

*Montrer que :* $Q(\theta^{[r]};\theta^{[r-1]})−Q(\theta^{[r-1]};\theta^{[r-1]})≥0$

$$
Q(\theta^{[r]};\theta^{[r-1]}) = \max_{\theta \in \Theta} Q(\theta;\theta^{[r-1]})
$$
en effet, par construction de l'algorithme EM
$$
\theta^{[r]} = \arg\max_{\theta \in \Theta} \sum_{i=1}^{n}\sum_{k=1}^{K}t_{i,k}(\theta^{[r-1]})ln(π_kp_k(x_i;α_k)) = \arg\max_{\theta \in \Theta} E_{\theta^{[r-1]}}[l(θ;x,z)|X_i=x_i]
$$
et $Q(θ;\theta^{[r-1]}) =E_{\theta^{[r-1]}}[l(θ;x,z)|X_i=x_i]$
La quantité $Q$ n'est rien d'autre que la vraissemblance complété calculée avec $\theta^{[r-1]}$
$$
\implies Q(\theta^{[r]};\theta^{[r-1]}) ≥ Q(\theta^{[r-1]};\theta^{[r-1]})
$$


*En utilisant l’[inégalité de Jensen](https://fr.wikipedia.org/wiki/In%C3%A9galit%C3%A9_de_Jensen), montrer que :* $H(\theta^{[r]};\theta^{[r-1]})−H(\theta^{[r-1]};\theta^{[r-1]})≤0$

$$
H(\theta^{[r]};\theta^{[r-1]})−H(\theta^{[r-1]};\theta^{[r-1]})
$$
$$
=\sum_{i=1}^n\sum_{k=1}^nE_{\theta^{[r-1]}}[z_{i,k}ln(t_{ik}(\theta^{[r]}))|X_i=x_i] - \sum_{i=1}^n\sum_{k=1}^nE_{\theta^{[r-1]}}[z_{i,k}ln(t_{ik}(\theta^{[r-1]}))|X_i=x_i]
$$

Attention : $ln(t_{ik}(\theta^{quelconque}))$ est déterministe ! La seule chose aléatoire dans les espérance ce sont les $z_{i,k}$

$$
=\sum_{i=1}^n\sum_{k=1}^n ln(t_{ik}(\theta^{[r]})) E_{\theta^{[r-1]}}[z_{i,k}|X_i=x_i] - \sum_{i=1}^n\sum_{k=1}^n ln(t_{ik}(\theta^{[r-1]})) E_{\theta^{[r-1]}}[z_{i,k}|X_i=x_i]
$$
et $E_{\theta^{[r-1]}}[z_{i,k}|X_i=x_i]$ est la définition de $t_{i,k}(\theta^{[r-1]})$
$$
=\sum_{i=1}^n\sum_{k=1}^n t_{ik}(\theta^{[r-1]})[ln(t_{ik}(\theta^{[r]})) - ln(t_{ik}(\theta^{[r-1]}))]
$$
$$
=\sum_{i=1}^n\sum_{k=1}^n t_{ik}(\theta^{[r-1]})ln(\frac{t_{ik}(\theta^{[r]})}{t_{ik}(\theta^{[r-1]})})
$$

On utilise Jensen et la concavité du logarithme ainsi :
$$
\sum_{k=1}^Ku_kln(v_k) \leq ln(\sum_{k=1}^Ku_kv_k)
$$
si les $u_k$ positifs et $\sum u_k=1$

$t_{ik}(\theta^{[r-1]}) \geq 0$ et $\sum_k t_{ik}(\theta^{[r-1]})=1$ car i appartient forcément à une des classes, donc la somme des probabilités d'appartenance à chacune des classes vaut 1

On remplace donc $u_k$ par $t_{ik}(\theta^{[r-1]})$ et $v_k$ par $\frac{t_{ik}(\theta^{[r]})}{t_{ik}(\theta^{[r-1]})}$ et on conclue

$$
H(\theta^{[r]};\theta^{[r-1]})−H(\theta^{[r-1]};\theta^{[r-1]})≤\sum_{i=1}^nln(\sum_{k=1}^Kt_{ik}(\theta^{[r]}))=0
$$


En cumulant les deux résultats précédents, on aboutit à 
$$
l(\theta^{[r]};x)-l(\theta^{[r-1]};x)\geq 0 \iff l(\theta^{[r]};x) \geq l(\theta^{[r-1]};x)
$$

On obtient qu'à chaque itération la vraissemblance augmente forcément, ce qui assure que l'algorithme va forcément converger vers un maximum local. (Au pire on stagne, ce qui sgnifie qu'on a atteint ce maximum)

# Exercice 4 : Application du modèle de mélange : loi de Poisson

La [loi de Poisson](https://fr.wikipedia.org/wiki/Loi_de_Poisson) est une loi discrète définie par $p(X=x)=\frac{\lambda^x}{x!}e^{-\lambda}$
Elle posède donc un paramètre : $\lambda$

On considère un échantillon $x= (x_1,...,x_n)$ composé de $n$ observations indépendantes $x_i∈\mathbb{N}$.  Pour effectuer le clustering, on suppose que les données sont issues d’un mélange de distributions de Poisson à $K$ composantes.

Si on mélange $K$ lois de poisson, on a donc $2K$ paramètres à estimer, $K$ $\lambda_k$ et $K$ $\pi_k$ (donc un forcé par contrainte $\sum \pi_k =1$)
$\theta = (\lambda_1,...,\lambda_K,\pi_1,...,\pi_K)$

Écriture générale
$$
p(x_i;\theta) = \sum_{k=1}^K \pi_k p_k(x_i;\lambda_k)
$$
ici :
$$
p(x_i;\theta) = \sum_{k=1}^K \pi_k \frac{ {\lambda_k}^{x_i}}{x_i!}e^{-\lambda_k}
$$
Les $\lambda_k$ sont positifs, et différents 2 à 2 (si 2 sont identiques, c'est la même composante)

Dans ces conditions, le modèle est-il identifiable ?
C'est à dire :
si $\forall x \in \mathbb{N}, p(x,\theta)=p(x,\tilde \theta) \implies \theta = \tilde \theta$
Dans le cas d'un mélange l'unicité se définit "à permutation des composantes près"
Pour cela on choisit par exemple de trier les $\lambda_k$ du plus grand au plus petit : contrainte sur "l'ordre" des composantes

Supposons $\forall x \in \mathbb{N}, p(x,\theta)=p(x,\tilde \theta)$
On choisit que si $\lambda_1 \neq \tilde \lambda_1$ alors on "classe" $\theta$ et $\tilde \theta$ tel que $\lambda_1 > \tilde \lambda_1$, c'est à dire qu'on suppose $\lambda_1 \geq \tilde \lambda_1$

$$
p(x,\theta)=p(x,\tilde \theta)
$$
$$
\iff \sum_{k=1}^K \pi_k \frac{ {\lambda_k}^{x_i}}{x_i!}e^{-\lambda_k}=\sum_{k=1}^K \tilde \pi_k \frac{ {\tilde \lambda_k}^{x_i}}{x_i!}e^{-\tilde \lambda_k}
$$
$$
\iff \pi_1 \frac{ {\lambda_1}^{x_i}}{x_i!}e^{-\lambda_1} + \sum_{k=2}^K \pi_k \frac{ {\lambda_k}^{x_i}}{x_i!}e^{-\lambda_k}=\tilde \pi_1 \frac{ {\tilde \lambda_1}^{x_i}} {x_i!}e^{-\tilde \lambda_1} + \sum_{k=2}^K \tilde \pi_k \frac{ {\tilde \lambda_k}^{x_i}}{x_i!}e^{-\tilde \lambda_k}
$$
$$
\iff 1 + \sum_{k=2}^K \frac{\pi_k}{\pi_1} \frac{ {\lambda_k}^{x_i}}{ {\lambda_1}^{x_i}}e^{\lambda_1-\lambda_k}=\frac{\tilde \pi_1}{\pi_1} \frac{ {\tilde \lambda_1}^{x_i}}{ {\lambda_1}^{x_i}}e^{\lambda_1 - \tilde \lambda_1} + \sum_{k=2}^K \frac{\tilde \pi_k}{\pi_1} \frac{ {\tilde \lambda_k}^{x_i}}{ {\lambda_1}^{x_i}}e^{\lambda_1-\tilde \lambda_k}
$$
Par hypothèse, on a $\lambda_1>\lambda_k$ et $\lambda_1 \geq \tilde \lambda_1 > \tilde \lambda_k$
Donc :
$\forall k>1,\frac{\lambda_k}{\lambda_1}<1$
$\forall k>1,\frac{\tilde \lambda_k}{\lambda_1}<1$
Donc :
$\forall k>1,\lim_{x\to\infty}\frac{\pi_k}{\pi_1}(\frac{\lambda_k}{\lambda_1})^{x_i}e^{(\lambda_1-\lambda_k)}=0$
$\forall k>1,\lim_{x\to\infty}\frac{\pi_k}{\pi_1}(\frac{\tilde \lambda_k}{\lambda_1})^{x_i}e^{(\lambda_1-\tilde \lambda_k)}=0$

Soit en revenant à l'égalité précédente
$$
\iff 1 = \lim_{x\to\infty}\frac{\tilde \pi_1}{\pi_1} \frac{ {\tilde \lambda_1}^{x_i}}{ {\lambda_1}^{x_i}}e^{\lambda_1 - \tilde \lambda_1} 
$$
et
$$
\lim_{x\to\infty} \frac{\tilde \pi_1}{\pi_1} \frac{ {\tilde \lambda_1}^{x_i}}{ {\lambda_1}^{x_i}}e^{\lambda_1 - \tilde \lambda_1} = \frac{\tilde \pi_1}{\pi_1} \text{ si } \lambda_1 = \tilde \lambda_1
$$
$$
\lim_{x\to\infty} \frac{\tilde \pi_1}{\pi_1} \frac{ {\tilde \lambda_1}^{x_i}}{ {\lambda_1}^{x_i}}e^{\lambda_1 - \tilde \lambda_1} = 0\text{ si } \lambda_1 > \tilde \lambda_1
$$

Donc (par l'absurde) $\lambda_1 = \tilde \lambda_1$ et de fait $\pi_1 = \tilde \pi_1$

Une fois qu'on a montré le résultat pour ce premier paramètre on effectue le même raisonnement pour les paramètres suivant

## Estimation par maximum de vraissemblance

$$
l(\theta;x)=\sum_{i=1}^nln(\sum_{k=1}^n \pi_k \frac{\lambda_k^{x_i}}{x_i!}e^{-\lambda_k})
$$
$$
l(\theta;x,z)=\sum_{i=1}^n\sum_{k=1}^nz_{i,k}ln( \pi_k \frac{\lambda_k^{x_i}}{x_i!}e^{-\lambda_k})
$$
$$
=\sum_{i=1}^n\sum_{k=1}^nz_{i,k}(ln( \pi_k ) + x_iln(\lambda_k) - ln(x_i!) -\lambda_k)
$$

**Algorithme EM**

On choisit au hasard les $\pi_k^{[0]}$, tels que $0<\pi_k^{[0]}<1$ et $\sum \pi_k^{[0]} =1$
ainsi que les $\lambda_k^{[0]}$ positifs

On choisit un $\epsilon$ petit qui sera le seuil à partir du quel on cosidèrera que l'évolution est minime, et que l'on arrive ainsi au maximum

Soit un critère d'arrêt de l'algorithme
$l(\theta^{[r]};x) - l(\theta^{[r-1]};x)\leq\epsilon$

A chaque étape

- On détermine une estimation des $z_{ik}$, les $t_{ik}$ calculés à l'aide des apriori, cad les paramètres de l'itération précédente :
$$
t_{ik}(\theta^{[r-1]})=\frac{\pi_k^{[r-1]}p_k(x_i;\lambda_k^{[r-1]})}{\sum_l \pi_l^{[r-1]}p_l(x_i;\lambda_l^{[r-1]})}
$$

- On maximise la vraissemblance complétée que l'on sait désormais calculer
$l(\theta;x,z)$ non calculable car dépendant des $z_{ik}$ inconnus devient $l(\theta;x,t(\theta^{[r-1]}))$ 
avec $t(\theta^{[r-1]})$ l'ensemble des $t_{ik}(\theta^{[r-1]})$
Soit la recheche de 
$$
\theta^{[r]}=\arg\max_{\theta}l(\theta;x,t(\theta^{[r-1]}))=\arg\max_{\theta}\sum_{i=1}^n\sum_{k=1}^nt_{ik}(\theta^{[r-1]})ln( \pi_k \frac{\lambda_k^{x_i}}{x_i!}e^{-\lambda_k})
$$

*Calcul des $\lambda_k$*

$$
\frac{\partial}{\partial \lambda_k}l(\theta;x,t(\theta^{[r-1]}))= \sum_i t_{ik}(\theta^{[r-1]})\frac{\partial}{\partial \lambda_k}(ln(\pi_k) -ln(x_i!)+x_iln(\lambda_k)-\lambda_k)
$$
$$
= \sum_i t_{ik}(\theta^{[r-1]})(\frac{x_i}{\lambda_k}-1)
$$
:warning: les $t_{ik}(\theta^{[r-1]})$ ne dépendent pas de $\lambda_k$ (mais de $\lambda_k^{[r-1]})$ !
$$
\frac{\partial}{\partial \lambda_k}l(\theta;x,t(\theta^{[r-1]}))= 0 \iff \frac{1}{\lambda_k^{[r]}}\sum_i t_{ik}(\theta^{[r-1]})x_i = \sum_i t_{ik}(\theta^{[r-1]})
$$
$$
\iff \lambda_k^{[r]} = \frac{\sum_i t_{ik}(\theta^{[r-1]})x_i}{\sum_i t_{ik}(\theta^{[r-1]})} 
$$

*Calcul des $\pi_k$*

Il s'agit d'une estimation sous contrainte ($\sum_k \pi_k =1$), on utilise donc un lagrangien

$L(\theta,\mu)=l(\theta;x, t_{ik}(\theta^{[r-1]})) - \mu (\sum_k \pi_k - 1)$
$$
\frac{\partial}{\partial \pi_k} L(\theta) = \sum_i t_{ik}(\theta^{[r-1]}) \frac{\partial}{\partial \pi_k}(ln(\pi_k) -ln(x_i!)+x_iln(\lambda_k)-\lambda_k)  - \mu
$$
$$
= \sum_i \frac{t_{ik}(\theta^{[r-1]}) }{\pi_k} - \mu
$$
(dériver selon $\mu$ fait simplement retrouver la contrainte $\sum_k\pi_k=1$)
$$
\frac{\partial}{\partial \pi_k} L(\theta) = 0 \iff \pi_k^{[r]}=\frac{1}{\mu}\sum_i t_{ik}(\theta^{[r-1]})
$$
puis on a par contrainte
$$
\sum_k \pi_k^{[r]}=1=\frac{1}{\mu}\sum_k\sum_i t_{ik}(\theta^{[r-1]})
$$
par construction 
$$
\sum_k t_{ik}(\theta^{[r-1]}) = 1
$$
donc 
$$
\sum_k\sum_i t_{ik}(\theta^{[r-1]}) =n
$$
soit $\mu=n$ et
$$
\pi_k^{[r]}=\frac{1}{n}\sum_i t_{ik}(\theta^{[r-1]})
$$
Au final étant donné que les $t_{ik}$ sont les espérances d'appartenance à chacune des classes, la somme est donc l'espérance de l'effectif de chacune des classes et on ne fait donc que calculer une fréquence (espérance du nombre d'individu dans la classe divisé par n) !

*Itération suivante*

Connaissant les nouveaux paramètres de $\theta$ on peut calculer la nouvelle valeur de la vraissemblance $l(\theta^{[r]};x)$ que l'on compare à celle de l'itération précédente

### Remarque : algorithme CEM

C'est l'algorithme EM plus réaliste du point de vue de la classification.
Au lieu de remplacer les $z_{ik}$ par leur espérance $t_{ik}$, on effectue la classification, c'est à dire que l'on affecte chaque $i$ dans la classe où il est le plus probable, cad vérifiant $\max_kt_{ik}$
On remplace donc les $z_{ik}$ par des valeurs plus réelles, 1 si $i$ a été affecté à $k$ lors de l'itération $[r-1]$, 0 sinon.
Dans l'algorithme CEM, les $\pi_k^{[r]}$ sont les vrais proportions des classes formées à l'itération $[r-1]$

### Remarque : méthode aléatoire

Comme pour les k-means, la méthode peut aboutir à un maximum local. Il faut donc relancer plusieurs fois l'algorithme, et conserver le cas qui a donné le plus haut résultat de vraissemblance (le maximum des maximum locaux a des chances d'être le maximum global)

### Remarque : choisir le nombre de classes

On pourrait se dire que l'on choisit $K$ tel que le maximum de vraissemblance obtenu soit le meilleur possible.
Mais comme avec l'inertie intra des méthodes géométriques, mécaniquement en augmentant K, le maximum de vraissemblance sera toujours plus élevé.
En effet $K$ plus élevé signifie un plus grand nombre de paramètres, ce qui améliore forcément le modèle.
On utilise au final des critères qui pénalisent le nombre de paramètre, AIC et BIC. C'est le même raisonnement que lorsqu'on observe un coude dans les gains d'inertie intra, on se demande si l'ajout de paramètre est "rentable".

# Exercice 5 : Lien entre clustering géométrique et probabiliste

On considère un échantillon $x=(x1,...,xn)$ composé de $n$ observations  indépendantes. Chaque observation $x_i∈\mathbb{R}^d$ est décrite par $d$ variables continues.
Montrer que le clustering de ces données en $K$ classes effectué par un algorithme des Kmeans avec la métrique diagonale $M=diag(\frac{1}{s^2_1},...,\frac{1}{s^2_d})$ (**métrique inverse des variances**) est équivalent à un clustering effectué par un algorithme CEM considérant le modèle défini par la densité suivante :
$$
p(x_i;θ) =\sum_{k=1}^{K}\frac{1}{K}\prod_{j=1}^{d}\phi(x_{ij};μ_{kj},s^2_j)
$$
avec 
$$
\phi(x_{ij};μ_{kj},s^2_j)=\frac{1}{s_j\sqrt{2\pi}}e^{-\frac{1}{2}(\frac{x_{ij}-μ_{kj}}{s_j})^2}
$$
la densité d'une loi normale d'espérance $μ_{kj}$ et de variance $s^2_j$

- Vision géométrique : voir le premier exercice du TP ou l'on a créé 4 groupes de points avec des moyennes différentes
- Vision probabiliste : on observe une ditribution avec $K$ "cloches" superposées

**Clustering Kmeans**
Détermination de l'estimateur $(\tilde z,\tilde \mu)$, où les $\mu_k$ sont les centres obtenus et les $z_{ik}$ calculé selon les points dont $\mu_k$ est le plus proche
$$
(\tilde z,\tilde \mu) = \arg\min_{z,\mu} \sum_i\sum_k z_{ik} d^2_M(x_i,\mu_k)
$$
En effet on recherche la configuration selon laquelle l'inertie intra est la plus faible, càd telles que la somme de la somme des distances des points à leur baycentre est la plus faible
$$
 = \arg\min_{z,\mu} \sum_i\sum_k z_{ik} \sum_{j=1}^d\frac{(x_{ij} -\mu_{kj})^2}{s^2_j}
$$
le barycentre de classe k étant le point de coordonnées $\mu_k=(\mu_{k,1},...,\mu_{k,d})$

**Clustering CEM**
Détermination de l'estimateur $(\hat z,\hat \mu)$ obtenu par maximum de vraissemblance
$$
(\hat z,\hat \mu)=\arg\max_{z,\mu} \sum_i\sum_k z_{i_k}ln(\frac{1}{K}\prod_{j=1}^d\phi(x_{ij};μ_{kj},s^2_j))
$$
$$
=\arg\max_{z,\mu} \sum_i\sum_k z_{i_k}ln(\frac{1}{K}) +z_{i_k} \sum_{j=1}^dln(\phi(x_{ij};μ_{kj},s^2_j))
$$
$$
=\arg\max_{z,\mu} \sum_i\sum_k [ z_{i_k}ln(\frac{1}{K}) - z_{i_k} \frac{1}{2}\sum_{j=1}^dln(2\pi s_j^2) -z_{i_k} \frac{1}{2} \sum_{j=1}^d\frac{(x_{ij}-μ_{kj})^2}{s^2_j} ]
$$
$$
=\arg\max_{z,\mu}   nln(\frac{1}{K}) - n\frac{1}{2}\sum_{j=1}^dln(2\pi s_j^2) - \sum_i\sum_kz_{i_k} \frac{1}{2} \sum_{j=1}^d\frac{(x_{ij}-μ_{kj})^2}{s^2_j} 
$$
$$
=\arg\max_{z,\mu} - \sum_i\sum_kz_{i_k} \sum_{j=1}^d\frac{(x_{ij}-μ_{kj})^2}{s^2_j} 
$$
$$
=\arg\min_{z,\mu} \sum_i\sum_kz_{i_k} \sum_{j=1}^d\frac{(x_{ij}-μ_{kj})^2}{s^2_j} 
$$

