# 1. Mesure du rendement

Avant d'évaluer le talent d'un gérant, il faut savoir **mesurer correctement** le rendement de son portefeuille. Deux pièges : la façon de **moyenner** les rendements dans le temps, et la façon de traiter les **flux** (apports/retraits) qui ne dépendent pas du gérant.

## 1. Rendement sur une période

Le rendement en pourcentage sur une période rapporte le gain (plus-value + revenus) à la valeur de départ. Sur \(N\) périodes, on dispose de \(r_1, r_2, \dots, r_N\) qu'il faut résumer par une moyenne — mais laquelle ?

## 2. Moyenne arithmétique vs géométrique

La **moyenne arithmétique** est la simple moyenne des rendements :

$$
r_A = \frac{1}{N}\sum_{i=1}^{N} r_i
$$

Elle suppose un **rééquilibrage** au début de chaque période (ou l'absence de réinvestissement). Exemple : 10 % puis 5,66 % → \(r_A = 7{,}83\%\).

La **moyenne géométrique** (ou *time-weighted*) tient compte du **réinvestissement** (*buy-and-hold*) : 1 € devient \(1{,}10\) après un an, puis \(1{,}10 \times 1{,}0566 = 1{,}1616\). Le taux de croissance annuel composé \(r_G\) résout :

$$
(1+r_G)^N = (1+r_1)(1+r_2)\cdots(1+r_N) \quad\Longrightarrow\quad r_G = \Big[\textstyle\prod_{i}(1+r_i)\Big]^{1/N} - 1
$$

Sur l'exemple, \(r_G = 7{,}81\%\) : légèrement **inférieur** à l'arithmétique. C'est une règle générale (\(r_G \le r_A\)) : l'écart, le **frein de volatilité** (*volatility drag*), croît avec la dispersion des rendements. Le widget l'illustre — essaie une série volatile comme `50, -50` pour voir l'arithmétique tomber à 0 % alors que la géométrique est nettement négative.

<iframe src="../../widgets/arith-geo.html" width="100%" height="480" style="border:0; border-radius:8px;" loading="lazy"></iframe>

## 3. TWRR — Time-Weighted Rate of Return

Le **TWRR** mesure la capacité du gérant à faire fructifier chaque euro investi, **neutralisé des flux** qu'il ne contrôle pas. On découpe la période à chaque flux et on chaîne les rendements des sous-périodes :

$$
r = \left[\frac{MV_{t_1}}{MV_0}\times\frac{MV_{t_2}}{MV_{t_1}+C_{t_1}}\times\cdots\times\frac{MV_{t_n}}{MV_{t_{n-1}}+C_{t_{n-1}}}\right]-1
$$

où \(MV_t\) est la valeur de marché et \(C_t\) le flux à la date \(t\). En isolant chaque sous-période **juste avant** le flux, le TWRR efface l'effet du timing des apports : c'est le rendement **du gérant**.

!!! example "Exemple"
    Fonds à 100 m€ en début d'année, 110 m€ en fin d'année, avec un apport net de 5 m€ à mi-année alors qu'il valait 95 m€ juste avant. Sous-période 1 : 95/100 = −5 %. Sous-période 2 : 110/(95+5) = +10 %. TWRR = (0,95 × 1,10) − 1 = **+4,5 %**.

## 4. MWRR — Money-Weighted Rate of Return

Le **MWRR** est le **taux de rendement interne** (TRI) de l'ensemble des flux : le taux qui égalise la valeur actuelle des entrées et des sorties. C'est le rendement **réellement vécu par l'investisseur**, sensible au timing de ses apports.

$$
MV_1 = MV_0(1+r) + \sum_{i=1}^{n} CF_i\,(1+r)^{w_i}, \qquad w_i = \frac{CD - D_i}{CD}
$$

!!! example "Exemple"
    Achat d'une action à 50 $ ; un an plus tard, achat d'une 2ᵉ action à 53 $ et dividende de 2 $ ; en année 2, dividendes de 4 $ et revente des deux actions à 54 $ (108 $). On résout \(50 + \frac{53}{1+r} = \frac{2}{1+r} + \frac{112}{(1+r)^2}\) → **r = 7,117 %**.

## 5. TWRR ou MWRR ? Avantages et limites

| | TWRR | MWRR |
|---|------|------|
| Mesure | Le talent du **gérant** (neutre aux flux) | Le rendement réel de l'**investisseur** |
| Avantages | Record historique ; comparable entre gérants ; ignore les entrées/sorties | Rattaché aux euros réellement détenus ; rendement personnalisé |
| Limites | Calcul plus lourd (valorisation à chaque flux) | Très sensible au timing des flux ; non comparable entre gérants |

!!! tip "L'écart de comportement (point d'examen)"
    En comparant la performance géométrique des grands marchés et la performance *money-weighted* des investisseurs, on observe que **les rendements géométriques du marché dépassent les rendements money-weighted** des investisseurs : en moyenne, les investisseurs achètent au mauvais moment (après les hausses) et vendent au mauvais moment. Le marché n'est pas en cause — c'est le **timing des flux** qui détruit de la performance. D'où l'intérêt du TWRR pour juger le gérant, et du MWRR pour juger l'investisseur.
