<!-- .slide: class="slide" -->
# Notations et calcul

$Y$ Données centrées

Pondération $P$

$V=Y^TPY$ Matrice de variance-covariance

$M_{IV}$ Métrique inverse des variance





<!-- .slide: class="slide" -->
\begin{aligned}
\dot{x} &amp; = \sigma(y-x) \\
\dot{y} &amp; = \rho x - y - xz \\
\dot{z} &amp; = -\beta z + xy
\end{aligned}








<!-- .slide: class="slide" -->

M_{IV}=
\begin{pmatrix}
1/\sigma^2_{math} & 0 & 0 \\
0 & 1/\sigma^2_{musique} & 0 \\
0 & 0 &1/\sigma^2_{français}
\end{pmatrix}


$$
M^{1/2}_{IV}=
\begin{pmatrix}
1/\sigma_{math} & 0 & 0 \\
0 & 1/\sigma_{musique} & 0 \\
0 & 0 &1/\sigma_{français}
\end{pmatrix}
$$

$M^{1/2}_{IV}VM^{1/2}_{IV}$ Matrice de corrélation









<!-- .slide: class="slide" -->
# ACP normée









<!-- .slide: class="slide" -->
## Point de vue métrique inverse des variances

- Données : $Y$
- Métrique : $M_{IV}$
- Matrice d'inertie : $Y^TPYM_{IV}$
$$
=
\begin{pmatrix}
y_1^{math}/\sigma^2_{math} & y_1^{musique}/\sigma^2_{musique}& y_1^{francais}/\sigma^2_{francais} \\
y_2^{math}/\sigma^2_{math} & y_2^{musique}/\sigma^2_{musique}& y_2^{francais}/\sigma^2_{francais} \\
... & ... & ...
\end{pmatrix}
$$
- Distances : $y_i^TM_{IV}y_i$
$$
= \frac{1}{\sigma^2_{math}} y_{i,math}^2 + \frac{1}{\sigma^2_{musique}} y_{i,musique}^2 + \frac{1}{\sigma^2_{français}} y_{i,français}^2 
$$









<!-- .slide: class="slide" -->
## Point de vue utilisation des données réduites

- Données : $Z=YM_{IV}^{1/2}$
- Métrique : $I_3$
- Matrice d'inertie : $Z^TPZI_3 = M_{IV}^{1/2}Y^TPYM_{IV}^{1/2}$ : matrice de corrélation
- Distances : $z_i^TI_3z_i = (M^{1/2}_{IV}y_i)^T(M^{1/2}_{IV}y_i)=y_i^TM_{IV}y_i$
$$
= \left(\frac{1}{\sigma_{math}} y_{i,math}\right)^2 + \left(\frac{1}{\sigma_{musique}} y_{i,musique}\right)^2 + \left(\frac{1}{\sigma_{français}} y_{i,français}\right)^2 
$$


