% Hausaufgabe 16
% Carmen Seidler <seidlerc@students.uni-marburg.de>
% 2014-06-12

Falls die Umlaute in dieser und anderen Dateien nicht korrekt dargestellt werden, sollten Sie File > Reopen with Encoding > UTF-8 sofort machen (und auf jeden Fall ohne davor zu speichern), damit die Enkodierung korrekt erkannt wird! 




# Die nächsten Punkte sollten beinahe automatisch sein...
1. Kopieren Sie diese Datei in Ihren Ordner (das können Sie innerhalb RStudio machen oder mit Explorer/Finder/usw.) und öffnen Sie die Kopie. Ab diesem Punkt arbeiten Sie mit der Kopie. Die Kopie bitte `hausaufgabe16.Rmd` nennen und nicht `Kopie...`
2. Sie sehen jetzt im Git-Tab, dass die neue Datei als unbekannt (mit gelbem Fragezeichen) da steht. Geben Sie Git Bescheid, dass Sie die Änderungen in der Datei verfolgen möchten (auf Stage klicken).
3. Machen Sie ein Commit mit den bisherigen Änderungen (schreiben Sie eine sinnvolle Message dazu -- sinnvoll bedeutet nicht unbedingt lang) und danach einen Push.
4. Ersetzen Sie meinen Namen oben mit Ihrem. Klicken auf Stage, um die Änderung zu merken.
5. Ändern Sie das Datum auf heute. (Seien Sie ehrlich! Ich kann das sowieso am Commit sehen.)
6. Sie sehen jetzt, dass es zwei Symbole in der Status-Spalte gibt, eins für den Zustand im *Staging Area* (auch als *Index* bekannt), eins für den Zustand im Vergleich zum Staging Area. Sie haben die Datei modifiziert, eine Änderung in das Staging Area aufgenommen, und danach weitere Änderungen gemacht. Nur Änderungen im Staging Area werden in den Commit aufgenommen.
7. Stellen Sie die letzten Änderungen auch ins Staging Area und machen Sie einen Commit (immer mit sinnvoller Message!).
8. Vergessen Sie nicht am Ende, die Lizenz ggf. zu ändern!

# Diamonds are forever 
Bisher haben Sie von mir mehr oder weniger vollständige Analysen bekommen, bei denen Sie im Prinzip nur einzelne Schritte einfügen müssten. Es wird allerdings langsam Zeit, dass Sie eine eigenständige Analyse ausführen. Sie haben das bei der Analyse vom Priming Experiment mittels ANOVA fast gemacht, aber auch da haben Sie viel von mir vorgefertigt bekommen. Für die Aufgaben heute werden Sie den Datensatz `diamonds` aus `ggplot2` bearbeiten. Schauen Sie sich die Beschreibung des Datensatzes an


```r
`?`(diamonds)
```

<div style="border: 2px solid black; padding: 5px; font-size: 80%;">
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html><head><title>R: Prices of 50,000 round cut diamonds</title>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<link rel="stylesheet" type="text/css" href="">
</head><body>

<table width="100%" summary="page for diamonds"><tr><td>diamonds</td><td align="right">R Documentation</td></tr></table>

<h2>Prices of 50,000 round cut diamonds</h2>

<h3>Description</h3>

<p>A dataset containing the prices and other attributes of
almost 54,000 diamonds. The variables are as follows:
</p>


<h3>Format</h3>

<p>A data frame with 53940 rows and 10 variables</p>


<h3>Details</h3>

 <ul>
<li><p> price. price in US dollars
(\$326&ndash;\$18,823) </p>
</li>
<li><p> carat. weight of the diamond
(0.2&ndash;5.01) </p>
</li>
<li><p> cut. quality of the cut (Fair, Good,
Very Good, Premium, Ideal) </p>
</li>
<li><p> colour. diamond colour,
from J (worst) to D (best) </p>
</li>
<li><p> clarity. a measurement
of how clear the diamond is (I1 (worst), SI1, SI2, VS1,
VS2, VVS1, VVS2, IF (best)) </p>
</li>
<li><p> x. length in mm
(0&ndash;10.74) </p>
</li>
<li><p> y. width in mm (0&ndash;58.9) </p>
</li>
<li><p> z. depth
in mm (0&ndash;31.8) </p>
</li>
<li><p> depth. total depth percentage = z /
mean(x, y) = 2 * z / (x + y) (43&ndash;79) </p>
</li>
<li><p> table. width
of top of diamond relative to widest point (43&ndash;95) </p>
</li></ul>



</body></html>

</div>

Die Aufgabe ist: eine Ausgangsfrage und die darauf folgenden Anschlussfragen statistisch zu beantworten. Sie können auch einige kleinere Fragen als Gruppe behandeln. Sie haben frei Wahl von Methoden und Fragen, aber sie müssen natürlich zueinander passen!

Mögliche Ausgangsfragen sind unter anderem:

* Was bestimmt den Preis eines Diamenten?
* Was bestimmt das Gewicht eines Diamenten? Hat Farbe oder Klarheit eine Auswirkung daruf oder bloß Volumen?
* Gibt es einen Zusammenhang zwischen den verschieden Dimensionen ("Längen")? 
* Gibt es einen Zusammenhang zwischen Farbe und Klarheit? Zwischen Farbe und Carat? Zwischen Farbe und Tiefe?
* ...

*Vergessen Sie dabei nicht, dass wir bisher nur Methoden gelernt haben, wo die abhängige Variable zumindest intervallskaliert ist!*

Sie können sich auch [das *ggplot* Buch](http://dx.doi.org/10.1007/978-0-387-98141-3) zur Inspiration anschauen, v.a. Abbildungen 4.7, 4.8, 4.9, 5.2, 5.3, 5.4, 5.6, 5.14, 7.16, 9.1  und Kapitel 2.2-2.5 könnten inspirierend wirken. Den Code zur Erstellung der Figuren findet man immer im Haupttext.

**Originale Fragestellungen und Auswertungen werden mit Bonuspunkten belohnt!** 

Hier ein paar Grafiken (auch im Buch zu finden):

```r
ggplot(diamonds, aes(x = carat, y = price, color = color)) + geom_point()
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-41.png) 

```r
ggplot(diamonds, aes(x = carat, y = price, color = color)) + geom_point(alpha = 0.3)
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-42.png) 

```r
ggplot(diamonds, aes(x = carat, y = price, color = color)) + geom_point() + 
    facet_wrap(~color)
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-43.png) 


# Noch eine Überlegung
Haben Sie dabei explorativ oder konfirmativ gearbeitet? Was hat das für eine Auswirkung auf die Interpretation der Ergebnisse?


#Analyse

1) Was bestimmt den Preis eines Diamanten?
- Überlegung: Je mehr Karat ein Diamat hat, umso teurer ist er. Farbe, Schliff und Reinheit haben ebeso Auswirkungen auf den Preis 

--> plotten


```r
ggplot(diamonds, aes(x = carat, y = price)) + geom_point()
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-51.png) 

```r
ggplot(diamonds, aes(x = carat, y = price, color = color)) + geom_point(alpha = 0.5)
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-52.png) 

```r
ggplot(diamonds, aes(x = carat, y = price, color = cut)) + geom_point(alpha = 0.5)
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-53.png) 

```r
ggplot(diamonds, aes(x = carat, y = price, color = clarity)) + geom_point(alpha = 0.5)
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-54.png) 


--> Lineare Regression um die Beziehung von Karat und Preis darzustellen


```r
ggplot(diamonds, aes(x = carat, y = price)) + geom_point() + geom_smooth(method = "lm")
```

![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6.png) 

/ log. Skalen


```r
ggplot(diamonds, aes(x = carat, y = price)) + geom_point() + geom_smooth(method = "lm") + 
    scale_x_log10() + scale_y_log10()
```

![plot of chunk unnamed-chunk-7](figure/unnamed-chunk-7.png) 


Mit einer linearen Regression kann statistisch nachvollzogen werden, ob Karat ein Prädikator für den Preis ist.


```r
summary(lm(price ~ carat, diamonds))
```

```
## 
## Call:
## lm(formula = price ~ carat, data = diamonds)
## 
## Residuals:
##    Min     1Q Median     3Q    Max 
## -18585   -805    -19    537  12732 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)  -2256.4       13.1    -173   <2e-16 ***
## carat         7756.4       14.1     551   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 1550 on 53938 degrees of freedom
## Multiple R-squared:  0.849,	Adjusted R-squared:  0.849 
## F-statistic: 3.04e+05 on 1 and 53938 DF,  p-value: <2e-16
```


Abhängigkeit von Preis und Karakt ist signifikaten mit einem R^2 von 84.93% der Formel "price = -2256.4 + carat * 7756.4"

Damit ist nicht alle Varianz erklärt, denn der Preis eines Diamanten hängt nicht nur von dessen Karat ab.
Die log. Transformation der Daten erzeugt ein Modell mit einem noch besseren Fit, daher gibt es eher einen exponentiellen statt einem linearen Zusammenhang:


```r
summary(lm(log10(price) ~ log10(carat), diamonds))
```

```
## 
## Call:
## lm(formula = log10(price) ~ log10(carat), data = diamonds)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -0.6551 -0.0736 -0.0026  0.0723  0.5811 
## 
## Coefficients:
##              Estimate Std. Error t value Pr(>|t|)    
## (Intercept)  3.669207   0.000593    6191   <2e-16 ***
## log10(carat) 1.675817   0.001934     867   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 0.114 on 53938 degrees of freedom
## Multiple R-squared:  0.933,	Adjusted R-squared:  0.933 
## F-statistic: 7.51e+05 on 1 and 53938 DF,  p-value: <2e-16
```


Problem: Farbe, Schliff und Reinheit sind nicht numerisch skaliert, sodass eine lineare Regression nicht möglich ist. Die Hypothese, dass der Karatwert (=Gewicht des Diamanten x*0,2=xGramm) vom Volumen abhängt lässt sich bestätigen:


```r
summary(lm(carat ~ x + y + z, diamonds))
```

```
## 
## Call:
## lm(formula = carat ~ x + y + z, data = diamonds)
## 
## Residuals:
##    Min     1Q Median     3Q    Max 
## -2.281 -0.070 -0.028  0.059  3.817 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept) -1.56677    0.00234 -669.40   <2e-16 ***
## x            0.35905    0.00230  156.32   <2e-16 ***
## y            0.00515    0.00177    2.91   0.0036 ** 
## z            0.07838    0.00267   29.40   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 0.104 on 53936 degrees of freedom
## Multiple R-squared:  0.952,	Adjusted R-squared:  0.952 
## F-statistic: 3.54e+05 on 3 and 53936 DF,  p-value: <2e-16
```


2) ANOVA
- Überprüfung ob es einen preislichen Unterschied zwischen Farbe, Schliff und Reinheitsgraden gibt (unterschiedliche Gruppengröße=verzerrtes Ergebnis)


```r
summary(aov(price ~ color * cut * clarity, data = diamonds))
```

```
##                      Df   Sum Sq  Mean Sq F value Pr(>F)    
## color                 6 2.68e+10 4.47e+09  307.61 <2e-16 ***
## cut                   4 9.70e+09 2.42e+09  166.69 <2e-16 ***
## clarity               7 2.00e+10 2.86e+09  196.38 <2e-16 ***
## color:cut            24 1.84e+09 7.65e+07    5.26  8e-16 ***
## color:clarity        42 1.35e+10 3.22e+08   22.15 <2e-16 ***
## cut:clarity          28 1.61e+09 5.73e+07    3.94  1e-11 ***
## color:cut:clarity   164 4.28e+09 2.61e+07    1.79  2e-09 ***
## Residuals         53664 7.81e+11 1.45e+07                   
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```


-- Haupteffekte und Interaktionen sind signifikant = Auswirkung auf Preis des Diamanten

ABER:

- as.numeric für lineare Regression zeigt ein leicht anderes Ergebnis


```r
diamonds$cut.num <- as.numeric(diamonds$cut)
diamonds$color.num <- as.numeric(diamonds$color)
diamonds$clarity.num <- as.numeric(diamonds$clarity)
head(diamonds)
```

```
##   carat       cut color clarity depth table price    x    y    z cut.num
## 1  0.23     Ideal     E     SI2  61.5    55   326 3.95 3.98 2.43       5
## 2  0.21   Premium     E     SI1  59.8    61   326 3.89 3.84 2.31       4
## 3  0.23      Good     E     VS1  56.9    65   327 4.05 4.07 2.31       2
## 4  0.29   Premium     I     VS2  62.4    58   334 4.20 4.23 2.63       4
## 5  0.31      Good     J     SI2  63.3    58   335 4.34 4.35 2.75       2
## 6  0.24 Very Good     J    VVS2  62.8    57   336 3.94 3.96 2.48       3
##   color.num clarity.num
## 1         2           2
## 2         2           3
## 3         2           5
## 4         6           4
## 5         7           2
## 6         7           6
```

```r

summary(lm(price ~ carat * color.num * cut.num, data = diamonds))
```

```
## 
## Call:
## lm(formula = price ~ carat * color.num * cut.num, data = diamonds)
## 
## Residuals:
##    Min     1Q Median     3Q    Max 
## -14010   -787    -19    636  12038 
## 
## Coefficients:
##                         Estimate Std. Error t value Pr(>|t|)    
## (Intercept)             -2362.38     110.25  -21.43  < 2e-16 ***
## carat                    7484.12     124.24   60.24  < 2e-16 ***
## color.num                 -32.88      27.01   -1.22     0.22    
## cut.num                   -68.88      26.76   -2.57     0.01 *  
## carat:color.num          -183.98      26.87   -6.85  7.6e-12 ***
## carat:cut.num             510.13      31.36   16.27  < 2e-16 ***
## color.num:cut.num           9.61       6.57    1.46     0.14    
## carat:color.num:cut.num   -34.34       6.77   -5.07  4.0e-07 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 1430 on 53932 degrees of freedom
## Multiple R-squared:  0.871,	Adjusted R-squared:  0.871 
## F-statistic: 5.21e+04 on 7 and 53932 DF,  p-value: <2e-16
```

Aus der linearen Regression geht, im Gegensatz zur ANOVA, hervor, dass die Farbe eines Diamanten scheinbar doch keinen Einfluss auf den Preis hat. 

# Lizenz
Dieses Werk ist lizenziert unter einer CC-BY-NC-SA Lizenz.
