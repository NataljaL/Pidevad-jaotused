---
title       : Pidevad jaotused
description : Siin tutvume põhiliste pidevate jaotuste- ning  kvantiilidega


--- type:NormalExercise lang:r xp:100 skills:1 key:af3c1cf198
## Normaaljaotus (1)

Normaaljaotus on kõige levinuim pidev jaotus statistikas. Normaaljaotusel on kaks parameetrit (keskväärtus $\mu$ ja standardhälve $\sigma$), mis määravad jaotuse asukohta $x$-telje suhtes ning jaotuse kuju. Paljud inimkehaga seotud mõõtmised on normaaljaotusega. Näiteks, fikseerides ära mingi küla kõikide meeste pikkuseid, on need normaaljaotusega.

Antud harjutuses keskendume funktsioonile `rnorm()`. Selle abil saab genereerida  normaaljaotusest mitut väärtust korraga etteantud parameetritega. Nende väärtuste kohta ütleme edaspidi **valim**.

*** =instructions

* Tee läbi käsk, mis vastab muutujale `norm_valim`. Pane tähele, millega võrduvad  selles käsus jaotuse keskväärtus ja standardhälve.
* Joonista saadud valimi põhjal histogramm (vastav käsk on juba kirjutatud). Kas märkasid normaaljaotuse kuju?
* Leia saadud valimi  põhjal  keskmine (käsuga `mean()`) ja standardhälve (käsuga `sd()`). Sulgudes ikka vastav väärtuste vektor.
* Muuda käsus `rnorm()` parameetri `mean` väärtust 35-ks ja tee käsud uuesti läbi. Mis juhtub normaaljaotusega?
* Muuda käsus `rnorm()` parameetri `sd` väärtust 0.1-ks ja tee käsud uuesti läbi. Mis juhtub normaaljaotusega nüüd?

*** =hint

* Argument `breaks` määrab histogrammis tulpade arvu (alati ei ole võimalik saavutada etteantud tulpade arvu, seetõttu võib tulla neid mõnevõrra rohkem või vähem).
* Valimikeskmise leidmiseks kasuta `mean(norm_valim)`.
* Valimi standardhälbe saamiseks kasuta `sd(norm_valim)`.

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# Valim mahuga 500 elementi normaaljaotusest:
norm_valim <- rnorm(500, mean = 5, sd = 2.5)

# Histogramm valimi põhjal:
hist(norm_valim, breaks = 50)

# Valimikeskmine:


# Valimi standardhälve:


```

*** =solution
```{r}
# Valim mahuga 500 elementi normaaljaotusest:
norm_valim <- rnorm(500, mean = 35, sd = 0.1)

# Histogramm valimi põhjal:
hist(norm_valim, breaks = 50)

# Valimikeskmine:
mean(norm_valim)

# Valimi standardhälve:
sd(norm_valim)

```

*** =sct
```{r}

# submission correctness tests
test_function("mean", incorrect_msg = "Kas arvutasid keskmise valimi `norm_valim` põhjal?")
test_function("sd", incorrect_msg = "Kas arvutasid standardhälbe valimi `norm_valim` põhjal?")

test_error()

# Final message the student will see upon completing the exercise
success_msg("Hea töö!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:360222386c
## Normaaljaotus (2)

Alati on kasulik teada kõiki valemeid, mille abil saab leida vajalikku tõenäosust. Kuid reaalses elus me üsna harva teostame arvututsi käsitsi. Ja miks ka peaks? `R`-is on selle jaoks vajalikud käsud olemas!

Normaaljaotusega on `R`-is seotud järgmised käsud:

* `dnorm()`: normaaljaotuse tihedusfunktsiooni $f(x)$ väärtus,
* `pnorm()`: normaaljaotuse jaotusfunktsiooni $F(x)=P(X\leq x)$ väärtus,
* `qnorm()`: normaaljaotuse kvantiil,
* `rnorm()`: (pseudo) juhuslik valim normaaljaotusest.

Eelmises harjutused juba kasutasid funktsiooni `rnorm()`. Funktsiooni `pnorm()` saab kasutada tõenäosuste leidmiseks. Uurime, kuidas see töötab!

*** =instructions

* Muutuja `pikkused` sisaldab 100 juhuslikult valitud täiskasvanu mehe pikkuse näitajat.
* Selle pikkuse jaotus sarnaneb normaaljaotusega (vt pikkuste histogrammi ning punast normaaljaotuse tiheduse kõverat -- väga sarnaste kujudega!)
* Kasutades normaaljaotust saab näiteks leida tõenäosust, et juhuslikult valitud täiskasvanu mehe pikkus on alla 165 cm või sellega võrdne (käsk on juba olemas, tee läbi).
* Kasutades sama normaaljaotust, leia tõenäosus, et juhuslikult valitud mehe pikkus on üle 190 cm (saab kasutada sama käsku, muutes vastavalt argumendi `lower.tail`).
* Leia tõenäosus, et pikkus jääb poollõiku (185, 195] cm (tuleta meelde, et $P(a<X\leq b)=F(b)-F(a)$).

*** =hint

* Abi käsu kasutamise kohta saab  `?pnorm` või  `help(pnorm)` abil.
* Keskväärtuse ja standardhälbe jaoks funktsioonis `pnorm()`  tuleb kasutada `mean(pikkused)` ja `sd(pikkused)`.
* Ära unustada kasutada argumenti `lower.tail`. See määrab jaotusel seda poolt, mille kohta tõenäosust soovid leida. Kui `lower.tail=TRUE`, siis leitakse `P(X<=x)`, vastasel juhul `FALSE` tõenäosuse `P(X>x)` leidmiseks.

*** =pre_exercise_code
```{r}
set.seed(44)
pikkused <- round(rnorm(100, 175, 5))
hist(pikkused, freq = F, col='orange', breaks=10, main="")
x<-seq(155, 205, 0.1)
lines(x, dnorm(x, mean(pikkused), sd(pikkused)), type="l", col="orangered", lwd=2)

```

*** =sample_code
```{r}
# Tõenäosus, et pikkus on <= 165:
t1 <- pnorm(165, mean = mean(pikkused), sd = sd(pikkused), lower.tail = TRUE)
t1

# Tõenäosus, et pikkus on > 190:
t2 <- 
t2

# Tõenäosus, et pikkus jääb poollõiku poollõiku (185, 195] cm:
t3 <- 
t3

```

*** =solution
```{r}
# Tõenäosus, et pikkus on <= 165:
t1 <- pnorm(165, mean = mean(pikkused), sd = sd(pikkused), lower.tail = TRUE)
t1

# Tõenäosus, et pikkus on > 190:
t2 <-  pnorm(190, mean = mean(pikkused), sd = sd(pikkused), lower.tail = FALSE)
t2

# Tõenäosus, et pikkus jääb poollõiku poollõiku (185, 195] cm:
t3 <- pnorm(195, mean = mean(pikkused), sd = sd(pikkused), lower.tail = FALSE)-pnorm(185, mean = mean(pikkused), sd = sd(pikkused), lower.tail = TRUE)
t3

```

*** =sct
```{r}
test_object("t1", incorrect_msg = "Kontrolli muutujat `t1`!" )
test_object("t2", incorrect_msg = "Kontrolli muutujat `t2`!" )
test_object("t3", incorrect_msg = "Kontrolli muutujat `t3`!" )

# test if the students code produces an error
test_error()

# Final message the student will see upon completing the exercise
success_msg("Tubli töö!")
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:059edb5e57
## Ühtlane jaotus

Eristatakse kahte tüüpi ühtlast jaotust: diskreetne ühtlane ja pidev ühtlane jaotus. Ühtlase jaotuse korral on kõikidel realisatsioonidel võrdne tõenäosus. 

Diskreetse ühtlase jaotusega on näiteks silmade arvud 1-st 6-ni ausa täringu veeretamisel. Igal realisatsioonil on tõenäosus 1/6. Pideva ühtlase jaotusega on näiteks Jüri bussi ootamise aeg, kui bussid käivad iga 10 minuti tagant ja Jüri tuleb bussipeatusse suvalisel hetkel.

Paremal on 4 graafikut (piltide kuvamine võib veidi aega võtta). Kas leiad, milline nendest vastab diskreetsele ühtlasele ja milline pidevale ühtlasele jaotusele? Ole tähelepanelik ka vertikaaltelje tähistusega!

*** =instructions

* Joonisel A on diskreetne ühtlane jaotus ja joonisel B on pideva ühtlase jaotuse tihedusfunktsioon.
* Ühtegi diskreetset jaotust siin pole, kuid joonisel C on pidev ühtlane jaotus.
* Joonisel D on diskreetne ühtlane jaotus ja joonisel  A on pidev ühtlane jaotus.
* Joonisel D on diskreetne ühtlane jaotus ja joonisel C on pidev ühtlane jaotus.

*** =hint

* Ühtlase jaotuse korral kõikidel $x$-väärtustel on võrdne tõenäosus diskreetsel juhul (või tihedusfunktsiooni väärtus pideval juhul).
* Joonisel  B on tegelikult kujutatud jaotusfunktsiooni graafik (küll pideva ühtlase jaotuse korral).
* Kui jaotus on diskreetne, siis tõenäosuse graafikul on "augud"".

*** =pre_exercise_code
```{r}
x <- seq(-5, 20, length = 50)
color<-"orange"
par(lwd=2, mfrow=c(2,2), cex.lab=1.5, cex.main=1.2)
plot(x, dunif(x, 0, 15), type='s', ylim=c(0,.15), col=color, ylab="f(x)", main='Joonis A')
plot(x, punif(x, 0, 15), type='l', col=color, ylab="F(x)", main='Joonis B')
plot(x, dnorm(x, 5, 2), type='l',col=color, ylab="f(x)", main='Joonis C')
plot(x, dunif(x, 0, 15), type='h', ylim=c(0,.15), col=color, ylab="P(X=x)", main='Joonis D')

```

*** =sct
```{r}
msg1 = "Joonisel A pole kahjuks diskreetne jaotus. Joonisel B on küll pidev ühtlane jaotus, kuid $y$-teljel on jaotusfunktsioon $F(x)$, mitte tihedusfunktsioon $f(x)$."
msg2 = "Siiski üks diskreetne jaotus on siin olemas. Lisaks on joonisel C tegu normaaljaotusega."
msg3 = "Sul on absoluutne õigus! Suundu järgmise ülesande juurde."
msg4 = "Kahjuks joonisel C on tegu normaaljaotusega. Kuid sul on õigus joonise D suhtes!"

test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))

# Final message the student will see upon completing the exercise
success_msg("Ilusti tehtud!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:eb21f6818b
## Eksponentjaotus

Exponentjaotus sobib sageli üsna hästi sellistele nähtustele, mis kirjeldavad ooteaega sõltumatute sündmuste vahel. Näiteks ooteaeg kuni järgmise kliendini  veebipoes või ooteaeg kuni järgmise spämmini  serveris.

Exponentjaotuse jaoks on `R`-is olemas järgmised käsud:

* `dexp()`: eksponentjaotuse tihedusfunktsiooni $f(x)$ väärtus,
* `pexp()`: eksponentjaotuse jaotusfunktsiooni $F(x)=P(X\leq x)$ väärtus,
* `qexp()`: eksponentjaotuse kvantiil,
* `rexp()`: (pseudo) juhuslik valim eksponentjaotusest.

Olgu $X\sim Exp(\lambda)$, kus $X$ on ooteaeg kuni järgmise kliendi saabumiseni. Tuletame meelde, et keskmine ooteaeg on sel juhul $EX=1/\lambda$.

*** =instructions

* Muutuja `ooteaeg` sisaldab ooteaegu ühe päeva esimese 100 kliendi kohta (minutites) konkreetses poes. 
* Selle jaotus sarnaneb eksponentjaotusega (vt ooteaja histogrammi ning tumerohelist eksponentjaotuse tiheduse kõverat -- väga sarnaste kujudega!)
* Kasutades eksponentjaotust saab näiteks leida tõenäosust, et ooteaeg kuni järgmise kliendi saabumiseni on vähemalt 15 minutit (käsk on juba olemas, tee läbi).
* Kasutades sama eksponentjaotust, leia tõenäosus, et ooteaeg kuni kliendi saabumiseni on kuni 3 minutit (3 min kaasaarvatud). Pane tähele argumenti `lower.tail`!
* Leia nüüd tõenäosus, et ooteaeg kuni järgmise kliendi saabumiseni on vahemikus (2, 6] minutit (2 ei ole kaasaarvatud ja 6 on).

*** =hint

* Abi käsu kasutamise kohta saab  `?pexp` või  `help(pexp)` abil.
* Pane tähele, et eksponentjaotuse parameetriks on nn sündmuste intensiivsus $\lambda$ ühes ajaühikus, kusjuures $\lambda=1/EX$.
* Ära unustada kasutada argumenti `lower.tail`. See määrab jaotusel seda poolt, mille kohta tõenäosust soovid leida. Kui `lower.tail=TRUE`, siis leitakse `P(X<=x)`, vastasel juhul `FALSE` tõenäosuse `P(X>x)` leidmiseks.

*** =pre_exercise_code
```{r}
set.seed(3)
ooteaeg <- round(rexp(100, 0.2), 2)
hist(ooteaeg, freq = F, col='lightgreen', breaks=10, main="")
x<-seq(0, 20, 0.1)
lines(x, dexp(x, 1/mean(ooteaeg)), type="l", col="darkgreen", lwd=2)

```

*** =sample_code
```{r}
# Tõenäosus, et ooteaeg on vähemalt 15 minutit (X>=15):
t1 <- pexp(15, rate = 1/mean(ooteaeg), lower.tail = FALSE)
t1

# Tõenäosus, et ooteaeg on kuni 3 min k.a. (X<=3):
t2 <- 
t2

# Tõenäosus, et ooteaeg on vahemikus (2, 6]:
t3 <- 
t3

```

*** =solution
```{r}
# Tõenäosus, et ooteaeg on vähemalt 15 minutit (X>=15):
t1 <- pexp(15, rate = 1/mean(ooteaeg), lower.tail = FALSE)
t1

# Tõenäosus, et ooteaeg on kuni 3 min k.a. (X<=3):
t2 <- pexp(3, rate = 1/mean(ooteaeg), lower.tail = TRUE)
t2

# Tõenäosus, et ooteaeg on vahemikus (2, 6]:
t3 <- pexp(6, rate = 1/mean(ooteaeg), lower.tail = TRUE)-pexp(2, rate = 1/mean(ooteaeg), lower.tail = TRUE)
t3

```

*** =sct
```{r}
test_object("t1", incorrect_msg = "Kontrolli muutujat `t1`!" )
test_object("t2", incorrect_msg = "Kontrolli muutujat `t2`! Kas muutsid argumendi `lower.tail`?" )
test_object("t3", incorrect_msg = "Kontrolli muutujat `t3`! Kas kasutasid valemit P(a<X<=b)=P(X<=b)-P(X<=a)?" )

# test if the students code produces an error
test_error()

# Final message the student will see upon completing the exercise
success_msg("Suurepärane tulemus!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:4c30fd9cc2
## Jaotuse kvantiilid ja täiendkvantiilid

Oled ehk märkanud eelmistes harjutustes käske `qexp()` ja `qnorm()`. Nende abil saab leida vastava teoreetilise jaotuse kvantiili $q\_{\alpha}$ või täiendkvantiili $\bar{q}\_{\alpha}$.  Vaatame siin põhjalikumalt funktsiooni `qnorm()`, kuna normaaljaotuse kvantiili läheb hiljem vaja. 

Funktsioon `qnorm()` kasutab argumendina tõenäosuse väärtust $\alpha$ ning arvutab juhusliku suuruse $X$ (ehk $x$-telje) väärtust $q\_\alpha$, mis on juhusliku suuruse $X$ kvantiil (juhul kui `lower.tail=TRUE`), ja täiendkvantiili $\bar{q}\_\alpha$ (juhul kui `lower.tail=FALSE`). 

$\alpha$-kvantiili korral kehtib $P(X\leq q\_\alpha)=\alpha$ ja $\alpha$-täiendkvantiili korral: $P(X>\bar{q}\_\alpha)=\alpha$.

Analoogiliselt käsuga `pnorm()`  on ka funktsioonil  `qnorm()` vaikeargumendid `mean = 0` ja `sd = 1`, mis vastavad standardsele normaaljaotusele. Seda jaotust on ka kasutatud antud harjutuses.

*** =instructions

1. Uuri, kuidas on leitud järgmine tõenäosus: $P(X\leq -1.64)$  ja on ümardatud 2 kohani peale koma.
2. Uuri, kuidas on leitud kvantiil, mis vastab tõenäosusele 0.05. Kvantiili väärtust on samuti ümardatud. Käsuga `qnorm_plot(0.05)` saad joonise, mis vastab jaotusele $N(0,\, 1)$ ning leitud kvantiilile.
3. Leia tõenäosus $P(X\leq -1.96)$ ja ümarda 3 kohanii peale koma.
4. Leia kvantiil, mis vastab tõenäosusele 0.025 ja ümarda 2 kohani peale koma. Kuva see joonisel käsuga `qnorm_plot()`.
5. Leia täiendkvantiili väärtus, mis vastab tõenäosusele 0.05 ja ümarda 2 kohani peale koma. Võrdle punktis 2 leitud kvantiili väärtusega.

*** =hint

* Ära unusta lisada argumenti `lower.tail=FALSE` kui soovid leida täiendkvantiili.

*** =pre_exercise_code
```{r}
# pre exercise code here
qnorm_plot <- function(alpha, twoway = F) {
  par(mar = c(7,4,5,4))
  a <- alpha
  x <- (-50:50)/10
  y <- dnorm(x)
  q1 <- qnorm(a); q2 <- qnorm(1-a)
  
  # draw the plot
  if(twoway) alph <- "alpha/2 =" else alph <- "alpha ="
  main <- paste("Kvantiil ja sellele vastav pindala \n jaotuse N(0,1) korral \n",
                alph, a)
  plot(x, y, type ="l", main = main, xlab = "", yaxt = "n", ylab = "", xaxt = "n")
  axis(1, at = c(-3, -1, 0, 1, 3))
  # mark the critical values with ticks
  if(twoway) at <- c(q1, q2) else at <- q1
  axis(1, at = round(at,2) , col.ticks = "red", las = 2)
  
  # show the critical value with the call to qnorm()
  #mtext(paste0("- z = qnorm(",a,") = ",round(q1,2)),
   #     side=1, line = 4, cex = 1.5)
  
  # highlight critical regions, add matching percentages
  x1 <- x[x<=q1]; x2 <- x[x>=q2]
  if(twoway) {
    polygon(c(min(x1),x1, max(x1), min(x2), x2, max(x2)),
            c(0, dnorm(x1),0, 0, dnorm(x2), 0), col = "grey60")
      text(x = c(-3.5, 3.5), y = c(0.08,0.08), labels = paste0(a*100,"%"), cex = 1.5)
      text(x = 0, y = 0.08, labels=paste0(100*(1-alpha/2),"%"), cex = 1.5)
  } else {
    polygon(c(min(x1),x1, max(x1)),
            c(0, dnorm(x1), 0), col = "grey60")
      text(x = -3.5, y = 0.08, labels = paste0(a*100,"%"), cex = 1.5)
      text(x = 0, y = 0.08, labels=paste0(100*(1-alpha),"%"), cex = 1.5)
  }
}
```

*** =sample_code
```{r}
# Harjutuse jaoks on loodud funktsioon qnorm_plot().

# 1. P(X <= - 1.64)
round(pnorm(-1.64), digits = 2)

# 2. Millise q korral: P(X <= q) = 0.05
round(qnorm(0.05), digits = 2)
qnorm_plot(0.05) # Graafik

# 3. P(X <= -1.96)


# 4. Millise q korral: P(X <= q) = 0.025



# 5. Millise täiend(q) korral P(X >= täiend(q)) = 0.05


```

*** =solution
```{r}
# Harjutuse jaoks on loodud funktsioon qnorm_plot().

# 1. P(X <= - 1.64)
round(pnorm(-1.64), digits = 2)

# 2. Millise q korral: P(X <= q) = 0.05
round(qnorm(0.05), digits = 2)
qnorm_plot(0.05) # Graafik

# 3. P(X <= -1.96)
round(pnorm(-1.96), digits = 3)

# 4. Millise q korral: P(X <= q) = 0.025
round(qnorm(0.025), digits = 2)
qnorm_plot(0.025)

# 5. Millise täiend(q) korral P(X >= täiend(q)) = 0.05
round(qnorm(0.05, lower.tail=FALSE), digits = 2)

```

*** =sct
```{r}
test_output_contains("round(pnorm(-1.96), digits = 3)", incorrect_msg = "Küsitud tõenäosust saab leida funktsiooni `pnorm()` abil. Ära unusta ümardamist!")
test_output_contains("round(qnorm(0.025), digits = 2)", incorrect_msg = "Küsitud kvantiili saab leida funktsioon `qnorm()` abil. Ära unusta ümardamist!")
test_output_contains("round(qnorm(0.05, lower.tail=FALSE), digits = 2)", incorrect_msg = "Küsitud täiendkvantiili saab leida funktsioon `qnorm()` abil, milles kirjuta ka argumendina `lower.tail=FALSE`.")

test_error()
success_msg("Tubli töö! Ja ongi lisapraktikum läbi!")
```