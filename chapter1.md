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
test_function("mean", args=c("x"), incorrect_msg = "Kas arvutasid keskmise valimi `norm_valim` põhjal?")
test_function("sd", args=c("x"), incorrect_msg = "Kas arvutasid standardhälbe valimi `norm_valim` põhjal?")

test_error()

# Final message the student will see upon completing the exercise
success_msg("Hea töö!")
```
