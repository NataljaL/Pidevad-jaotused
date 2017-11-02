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
