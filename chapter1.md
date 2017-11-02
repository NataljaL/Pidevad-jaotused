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
* Kasutades normaaljaotust saab näiteks leida tõenäosust, et juhuslikult valitud täiskasvanu mehe pikkus on alla 165 cm (käsk on juba olemas, tee läbi).
* Kasutades sama normaaljaotust, leia tõenäosus, et juhuslikult valitud mehe pikkus on üle 190 cm (saab kasutada sama käsku, muutes vastavalt argumendi `lower.tail`).
* Leia tõenäosus, et pikkus jääb vaemikku 185-195 cm.

*** =hint

Look at the help pages with ?pnorm or help(pnorm).
Use the mean and standard deviation of variable deep as arguments for the pnorm() function.
Remember to use the lower.tail argument in the pnorm() function. It determines which "side" you are calculating. The lower.tail argument can be either TRUE or FALSE.

*** =pre_exercise_code
```{r}
set.seed(44)
x <- round(rnorm(100, 175, 5))
hist(learning2014$deep, freq = F, col='orange', ylim=c(0,.8))
x<-seq(0, 5, length = 50)
lines(x, dnorm(x, mean(learning2014$deep), sd(learning2014$deep)), type="l", col="orangered", lwd=2)

```

*** =sample_code
```{r}
# learning2014 is available

# Create object deep
deep <- learning2014$deep

# Approximate probability of deep being smaller than 3
pnorm(3, mean = mean(deep), sd = sd(deep), lower.tail = TRUE)

# Approximate probability of deep being greater than 3


# Approximate probability of deep being greater than 4.5
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
