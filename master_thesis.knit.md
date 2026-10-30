---
title: "Different Grievances, Same Vote: How Different Dimensions of Perceived Societal Misrecognition Shape Support for the Populist Radical Right."
author:
- Lisa Kauer
date: 'October 30, 2026'
output:
  html_document:
    toc: no
    df_print: paged
  html_notebook:
    fig_caption: yes
    toc: no
  word_document:
    toc: no
  pdf_document:
    fig_caption: yes
    toc: yes
header-includes:
- \usepackage{setspace}\doublespacing
- \usepackage{dcolumn} 
- \usepackage{rotating,graphicx} # for a nicer presentation of the tables in the pdf format
fontsize: 12pt
geometry: left=2.5cm,right=2.5cm,top=2.5cm,bottom=2.5cm
abstract: ".\\clearpage"
---













Data Manipulation 

```r
################################
# main variables
################################

######################
# dependent variable #
######################


#===================================
# vote choice: Zweitstimme - q114ba  
#===================================

# q114ba - Version A - because it contains all information we need
sort(unique(data$q114ba)) # get an overview 
```

```
## <labelled<double>[13]>: Wahlentscheidung: BTW 2025, Zweitstimme (Version A)
##  [1] -99 -98 -97 -83 -73   1   4   5   6   7 322 392 801
## 
## Labels:
##  value                                     label
##    -99                              keine Angabe
##    -98                               weiss nicht
##    -97                           trifft nicht zu
##    -96                                     Split
##    -95                        nicht teilgenommen
##    -94                nicht in Auswahlgesamtheit
##    -93                     Interview abgebrochen
##    -92                           Fehler in Daten
##    -91                                     Modus
##    -86                      nicht wahlberechtigt
##    -85                             nicht waehlen
##    -84           keine Erst-/Zweitstimme abgeben
##    -83                         ungueltig waehlen
##    -82               keine andere Partei waehlen
##    -81                    noch nicht entschieden
##    -73                         Mehrfachnennungen
##    -72                      nicht einzuschaetzen
##    -71                             nicht bekannt
##      1                                   CDU/CSU
##      2                                       CDU
##      3                                       CSU
##      4                                       SPD
##      5                                       FDP
##      6                                    GRUENE
##      7                                 DIE LINKE
##    116                                       BBP
##    120                                       BIG
##    122                                        BD
##    126                                        BP
##    127                                       BPD
##    146                               DIE FRANKEN
##    149                                DIE GRAUEN
##    150 Die Konservativen (Deutsche Konservative)
##    151                                Die PARTEI
##    152                             DIE VIOLETTEN
##    156                                       DKP
##    164                                       DSP
##    168                                       DVU
##    170                                    Eltern
##    171                                   FAMILIE
##    180                             FREIE WAEHLER
##    188                                       GUT
##    197                                       KPD
##    202                                      MLPD
##    205                   Partei der Nichtwaehler
##    206                                       NPD
##    207                                     NSDAP
##    209                                      oedp
##    210                                  OekoLinX
##    214                                       PBC
##    215                                   PIRATEN
##    218                           pro Deutschland
##    225                                       REP
##    229                                       SED
##    234                                       SSW
##    237                          Tierschutzpartei
##    249                           Volksabstimmung
##    256                                   ZENTRUM
##    304                                      LDPD
##    305                                       DBD
##    309                                      NDPD
##    310                                       PDV
##    313                              DIE FREIHEIT
##    315                                        B*
##    317                                        DL
##    318                                       GPD
##    322                                       AfD
##    326                                        NM
##    327                                       ADd
##    328                                      AVIP
##    331                                       LKR
##    335                          TIERSCHUTZ hier!
##    338                                       BGE
##    342                      Gesundheitsforschung
##    344                                 V-Partei³
##    345                         Tierschutzallianz
##    346                              Gartenpartei
##    348                                        DM
##    349                                       DiB
##    350                            Die Humanisten
##    351                                Buendnis C
##    352                                Die Urbane
##    353                                        NL
##    354                                       SGP
##    356                                       mut
##    357                             Graue Panther
##    359                                    DiEM25
##    360                                  III. Weg
##    361                                Die Grauen
##    362                                 Die Liebe
##    363                     PARTEI FUER DIE TIERE
##    364                                      Volt
##    365                       BVB / FREIE WAEHLER
##    368                              KlimalisteBW
##    369                             KlimalisteRLP
##    372                                  dieBasis
##    373                          Team Todenhoefer
##    374                                BUENDNIS21
##    376                                       PdF
##    378                           BUERGERBEWEGUNG
##    379                                       LfK
##    383                         Klimaliste Berlin
##    392                                       BSW
##    393                                WerteUnion
##    396                                      DAVA
##    800                                  Sonstige
##    801                             andere Partei
##    802                            Einzelkandidat
##    803                     Waehlergemeinschaften
##    804                 rechte Parteien allgemein
##    805                  linke Parteien allgemein
##    806                           kleine Parteien
##    808                              keine Partei
##    809                  alle Parteien gleich gut
##    810       mit mehreren Parteien/Unentschieden
##  NA(a)                              keine Angabe
##  NA(b)                               weiss nicht
##  NA(c)                           trifft nicht zu
##  NA(d)                                     Split
##  NA(e)                        nicht teilgenommen
##  NA(f)                nicht in Auswahlgesamtheit
##  NA(g)                     Interview abgebrochen
##  NA(h)                           Fehler in Daten
##  NA(i)                                     Modus
##  NA(j)                      nicht wahlberechtigt
##  NA(k)                             nicht waehlen
##  NA(l)           keine Erst-/Zweitstimme abgeben
##  NA(m)                         ungueltig waehlen
##  NA(n)               keine andere Partei waehlen
##  NA(o)                    noch nicht entschieden
##  NA(p)                      nicht einzuschaetzen
##  NA(q)                             nicht bekannt
##  NA(r)                         Mehrfachnennungen
```

```r
summary (data$q114ba) # summary statistics
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##  -99.00    1.00    4.00   68.46    7.00  801.00
```

```r
table(data$q114ba, useNA = "always") # frequencies 
```

```
## 
##  -99  -98  -97  -83  -73    1    4    5    6    7  322  392  801 <NA> 
##  243  287  357   26    9 1842 1015  282 1119  751  857  348  200    0
```

```r
# recode missing values 
data_clean$q114ba[data_clean$q114ba == -99] <- tagged_na("a")
data_clean$q114ba[data_clean$q114ba == -98] <- tagged_na("b")
data_clean$q114ba[data_clean$q114ba == -97] <- tagged_na("c")
data_clean$q114ba[data_clean$q114ba == -83] <- tagged_na("m")
data_clean$q114ba[data_clean$q114ba == -73] <- tagged_na("r")

# check if it worked 
table(data$q114ba, useNA = "always") # frequencies old 
```

```
## 
##  -99  -98  -97  -83  -73    1    4    5    6    7  322  392  801 <NA> 
##  243  287  357   26    9 1842 1015  282 1119  751  857  348  200    0
```

```r
table(data_clean$q114ba, useNA = "always") # frequencies new 
```

```
## 
##    1    4    5    6    7  322  392  801 <NA> 
## 1842 1015  282 1119  751  857  348  200  922
```

```r
summary (data_clean$q114ba)  
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
##    1.00    1.00    6.00   92.28    7.00  801.00     922
```

```r
d1$q114ba <- data_clean$q114ba # add cleaned variable to d1 

table(d1$q114ba, useNA = "always") # frequencies new
```

```
## 
##    1    4    5    6    7  322  392  801 <NA> 
## 1842 1015  282 1119  751  857  348  200  922
```

```r
# create new dummy variable: for vote choice -> AfD = 1
d1 <- d1 %>%
  mutate(
    afd_vote = case_when(
      q114ba == 322 ~ 1,
      q114ba %in% c(1, 4, 5, 6, 7, 392, 801) ~ 0,
      TRUE ~ NA_real_ ) )

table(d1$afd_vote, useNA = "always") #check if it worked // looks good
```

```
## 
##    0    1 <NA> 
## 5557  857  922
```

```r
##############################
# main independent variables #
##############################

# Societal Misrecognition: q46a-d
################################

#---------------------------
# (a) economic needs
#---------------------------
class(data$q46a)
```

```
## [1] "haven_labelled" "vctrs_vctr"     "double"
```

```r
unique(data$q46a) # get an overview 
```

```
## <labelled<double>[7]>: Abgehaengtheit: subjektiv, zu wenig Aufmerksamkeit fuer finanz. Lage
## [1]   1 -99   4   3   2   5 -93
## 
## Labels:
##  value                           label
##    -99                    keine Angabe
##    -98                     weiss nicht
##    -97                 trifft nicht zu
##    -96                           Split
##    -95              nicht teilgenommen
##    -94      nicht in Auswahlgesamtheit
##    -93           Interview abgebrochen
##    -92                 Fehler in Daten
##    -91                           Modus
##    -86            nicht wahlberechtigt
##    -85                   nicht waehlen
##    -84 keine Erst-/Zweitstimme abgeben
##    -83               ungueltig waehlen
##    -82     keine andere Partei waehlen
##    -81          noch nicht entschieden
##    -73               Mehrfachnennungen
##    -72            nicht einzuschaetzen
##    -71                   nicht bekannt
##      1         stimme voll und ganz zu
##      2                  stimme eher zu
##      3                     teils/teils
##      4            stimme eher nicht zu
##      5      stimme ueberhaupt nicht zu
##  NA(a)                    keine Angabe
##  NA(b)                     weiss nicht
##  NA(c)                 trifft nicht zu
##  NA(d)                           Split
##  NA(e)              nicht teilgenommen
##  NA(f)      nicht in Auswahlgesamtheit
##  NA(g)           Interview abgebrochen
##  NA(h)                 Fehler in Daten
##  NA(i)                           Modus
##  NA(j)            nicht wahlberechtigt
##  NA(k)                   nicht waehlen
##  NA(l) keine Erst-/Zweitstimme abgeben
##  NA(m)               ungueltig waehlen
##  NA(n)     keine andere Partei waehlen
##  NA(o)          noch nicht entschieden
##  NA(p)            nicht einzuschaetzen
##  NA(q)                   nicht bekannt
##  NA(r)               Mehrfachnennungen
```

```r
table(data$q46a, useNA = "always") # frequencies 
```

```
## 
##  -99  -93    1    2    3    4    5 <NA> 
##  212  164  515 1592 2344 1836  673    0
```

```r
summary (data$q46a) # statistics
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
## -99.000   2.000   3.000  -2.017   4.000   5.000
```

```r
# recode missing values 
data_clean$q46a[data_clean$q46a == -99] <- tagged_na("a")
data_clean$q46a[data_clean$q46a == -93] <- tagged_na("g")

#check if it worked 
table(data$q46a, useNA = "always") # frequencies old 
```

```
## 
##  -99  -93    1    2    3    4    5 <NA> 
##  212  164  515 1592 2344 1836  673    0
```

```r
table(data_clean$q46a, useNA = "always") # frequencies new 
```

```
## 
##    1    2    3    4    5 <NA> 
##  515 1592 2344 1836  673  376
```

```r
summary (data_clean$q46a)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
##    1.00    2.00    3.00    3.08    4.00    5.00     376
```

```r
#-----------------------
# (b) work 
#----------------------
sort(unique(data$q46b)) # get an overview 
```

```
## <labelled<double>[7]>: Abgehaengtheit: subjektiv, zu wenig Anerkennung fuer Arbeit
## [1] -99 -93   1   2   3   4   5
## 
## Labels:
##  value                           label
##    -99                    keine Angabe
##    -98                     weiss nicht
##    -97                 trifft nicht zu
##    -96                           Split
##    -95              nicht teilgenommen
##    -94      nicht in Auswahlgesamtheit
##    -93           Interview abgebrochen
##    -92                 Fehler in Daten
##    -91                           Modus
##    -86            nicht wahlberechtigt
##    -85                   nicht waehlen
##    -84 keine Erst-/Zweitstimme abgeben
##    -83               ungueltig waehlen
##    -82     keine andere Partei waehlen
##    -81          noch nicht entschieden
##    -73               Mehrfachnennungen
##    -72            nicht einzuschaetzen
##    -71                   nicht bekannt
##      1         stimme voll und ganz zu
##      2                  stimme eher zu
##      3                     teils/teils
##      4            stimme eher nicht zu
##      5      stimme ueberhaupt nicht zu
##  NA(a)                    keine Angabe
##  NA(b)                     weiss nicht
##  NA(c)                 trifft nicht zu
##  NA(d)                           Split
##  NA(e)              nicht teilgenommen
##  NA(f)      nicht in Auswahlgesamtheit
##  NA(g)           Interview abgebrochen
##  NA(h)                 Fehler in Daten
##  NA(i)                           Modus
##  NA(j)            nicht wahlberechtigt
##  NA(k)                   nicht waehlen
##  NA(l) keine Erst-/Zweitstimme abgeben
##  NA(m)               ungueltig waehlen
##  NA(n)     keine andere Partei waehlen
##  NA(o)          noch nicht entschieden
##  NA(p)            nicht einzuschaetzen
##  NA(q)                   nicht bekannt
##  NA(r)               Mehrfachnennungen
```

```r
summary (data$q46b) # summary statistics
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
## -99.000   2.000   3.000  -2.723   4.000   5.000
```

```r
table(data$q46b, useNA = "always") # frequencies 
```

```
## 
##  -99  -93    1    2    3    4    5 <NA> 
##  260  164  688 1763 1822 1861  778    0
```

```r
# recode missing values 
data_clean$q46b[data_clean$q46b == -99] <- tagged_na("a")
data_clean$q46b[data_clean$q46b == -93] <- tagged_na("g")

#check if it worked 
table(data$q46b, useNA = "always") # frequencies old 
```

```
## 
##  -99  -93    1    2    3    4    5 <NA> 
##  260  164  688 1763 1822 1861  778    0
```

```r
table(data_clean$q46b, useNA = "always") # frequencies new 
```

```
## 
##    1    2    3    4    5 <NA> 
##  688 1763 1822 1861  778  424
```

```r
summary (data_clean$q46b)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
##    1.00    2.00    3.00    3.04    4.00    5.00     424
```

```r
#--------------------------------------
# (c) basic infrastructure and services
#--------------------------------------
unique(data$q46c) # get an overview 
```

```
## <labelled<double>[7]>: Abgehaengtheit: subjektiv, zu wenig Zugang zu grundlegender Infrastruktur
## [1]   4 -99   3   2   1   5 -93
## 
## Labels:
##  value                           label
##    -99                    keine Angabe
##    -98                     weiss nicht
##    -97                 trifft nicht zu
##    -96                           Split
##    -95              nicht teilgenommen
##    -94      nicht in Auswahlgesamtheit
##    -93           Interview abgebrochen
##    -92                 Fehler in Daten
##    -91                           Modus
##    -86            nicht wahlberechtigt
##    -85                   nicht waehlen
##    -84 keine Erst-/Zweitstimme abgeben
##    -83               ungueltig waehlen
##    -82     keine andere Partei waehlen
##    -81          noch nicht entschieden
##    -73               Mehrfachnennungen
##    -72            nicht einzuschaetzen
##    -71                   nicht bekannt
##      1         stimme voll und ganz zu
##      2                  stimme eher zu
##      3                     teils/teils
##      4            stimme eher nicht zu
##      5      stimme ueberhaupt nicht zu
##  NA(a)                    keine Angabe
##  NA(b)                     weiss nicht
##  NA(c)                 trifft nicht zu
##  NA(d)                           Split
##  NA(e)              nicht teilgenommen
##  NA(f)      nicht in Auswahlgesamtheit
##  NA(g)           Interview abgebrochen
##  NA(h)                 Fehler in Daten
##  NA(i)                           Modus
##  NA(j)            nicht wahlberechtigt
##  NA(k)                   nicht waehlen
##  NA(l) keine Erst-/Zweitstimme abgeben
##  NA(m)               ungueltig waehlen
##  NA(n)     keine andere Partei waehlen
##  NA(o)          noch nicht entschieden
##  NA(p)            nicht einzuschaetzen
##  NA(q)                   nicht bekannt
##  NA(r)               Mehrfachnennungen
```

```r
summary (data$q46c) # summary statistics
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##  -99.00    3.00    4.00   -2.12    5.00    5.00
```

```r
table(data$q46c, useNA = "always") # frequencies 
```

```
## 
##  -99  -93    1    2    3    4    5 <NA> 
##  262  164  299  806 1487 2326 1992    0
```

```r
# recode missing values 
data_clean$q46c[data_clean$q46c == -99] <- tagged_na("a")
data_clean$q46c[data_clean$q46c == -93] <- tagged_na("g")

#check if it worked 
table(data$q46c, useNA = "always") # frequencies old 
```

```
## 
##  -99  -93    1    2    3    4    5 <NA> 
##  262  164  299  806 1487 2326 1992    0
```

```r
table(data_clean$q46c, useNA = "always") # frequencies new 
```

```
## 
##    1    2    3    4    5 <NA> 
##  299  806 1487 2326 1992  426
```

```r
summary (data_clean$q46c)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
##    1.00    3.00    4.00    3.71    5.00    5.00     426
```

```r
#------------------------------------
# (d) opinion  
#------------------------------------
unique(data$q46d) # get an overview 
```

```
## <labelled<double>[7]>: Abgehaengtheit: subjektiv, keine freie Meinungsaeusserung moeglich
## [1]   4 -99   5   3   1   2 -93
## 
## Labels:
##  value                           label
##    -99                    keine Angabe
##    -98                     weiss nicht
##    -97                 trifft nicht zu
##    -96                           Split
##    -95              nicht teilgenommen
##    -94      nicht in Auswahlgesamtheit
##    -93           Interview abgebrochen
##    -92                 Fehler in Daten
##    -91                           Modus
##    -86            nicht wahlberechtigt
##    -85                   nicht waehlen
##    -84 keine Erst-/Zweitstimme abgeben
##    -83               ungueltig waehlen
##    -82     keine andere Partei waehlen
##    -81          noch nicht entschieden
##    -73               Mehrfachnennungen
##    -72            nicht einzuschaetzen
##    -71                   nicht bekannt
##      1         stimme voll und ganz zu
##      2                  stimme eher zu
##      3                     teils/teils
##      4            stimme eher nicht zu
##      5      stimme ueberhaupt nicht zu
##  NA(a)                    keine Angabe
##  NA(b)                     weiss nicht
##  NA(c)                 trifft nicht zu
##  NA(d)                           Split
##  NA(e)              nicht teilgenommen
##  NA(f)      nicht in Auswahlgesamtheit
##  NA(g)           Interview abgebrochen
##  NA(h)                 Fehler in Daten
##  NA(i)                           Modus
##  NA(j)            nicht wahlberechtigt
##  NA(k)                   nicht waehlen
##  NA(l) keine Erst-/Zweitstimme abgeben
##  NA(m)               ungueltig waehlen
##  NA(n)     keine andere Partei waehlen
##  NA(o)          noch nicht entschieden
##  NA(p)            nicht einzuschaetzen
##  NA(q)                   nicht bekannt
##  NA(r)               Mehrfachnennungen
```

```r
summary (data$q46d) # summary statistics
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
## -99.000   3.000   4.000  -1.454   5.000   5.000
```

```r
table(data$q46d, useNA = "always") # frequencies 
```

```
## 
##  -99  -93    1    2    3    4    5 <NA> 
##  229  164  387  699 1081 1650 3126    0
```

```r
# recode missing values 
data_clean$q46d[data_clean$q46d == -99] <- tagged_na("a")
data_clean$q46d[data_clean$q46d == -93] <- tagged_na("g")

#check if it worked 
table(data$q46d, useNA = "always") # frequencies old 
```

```
## 
##  -99  -93    1    2    3    4    5 <NA> 
##  229  164  387  699 1081 1650 3126    0
```

```r
table(data_clean$q46d, useNA = "always") # frequencies new 
```

```
## 
##    1    2    3    4    5 <NA> 
##  387  699 1081 1650 3126  393
```

```r
summary (data_clean$q46d)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
##   1.000   3.000   4.000   3.926   5.000   5.000     393
```

```r
#------------------------------------------------------------------------------

# add new cleaned variables to d1
d1$q46a <- data_clean$q46a 
d1$q46b <- data_clean$q46b
d1$q46c <- data_clean$q46c
d1$q46d <- data_clean$q46d

# create 4 new misrecognition variables with new scale ranging from 0 to 1
# recoded scale: 
# 1 =  strongly agree
# 0.75 = agree
# 0.5 = neither
# 0.25 = disagree
# 0 = strongly disagree

d1 <- d1 %>%
  mutate(
    misrec_economic       = (5 - q46a) / 4,
    misrec_work           = (5 - q46b) / 4,
    misrec_services       = (5 - q46c) / 4,
    misrec_opinion        = (5 - q46d) / 4)

#check if it worked:

# misrecognition of economic needs
table(d1$q46a, useNA = "always") # frequencies old 
```

```
## 
##    1    2    3    4    5 <NA> 
##  515 1592 2344 1836  673  376
```

```r
table(d1$misrec_economic, useNA = "always") # frequencies new
```

```
## 
##    0 0.25  0.5 0.75    1 <NA> 
##  673 1836 2344 1592  515  376
```

```r
table(d1$q46a,d1$misrec_economic, useNA = "always") # compare
```

```
##       
##           0 0.25  0.5 0.75    1 <NA>
##   1       0    0    0    0  515    0
##   2       0    0    0 1592    0    0
##   3       0    0 2344    0    0    0
##   4       0 1836    0    0    0    0
##   5     673    0    0    0    0    0
##   <NA>    0    0    0    0    0  376
```

```r
# misrecognition of work
table(d1$q46b, useNA = "always") # frequencies old 
```

```
## 
##    1    2    3    4    5 <NA> 
##  688 1763 1822 1861  778  424
```

```r
table(d1$misrec_work, useNA = "always") # frequencies new
```

```
## 
##    0 0.25  0.5 0.75    1 <NA> 
##  778 1861 1822 1763  688  424
```

```r
table(d1$q46b,d1$misrec_work, useNA = "always") # compare
```

```
##       
##           0 0.25  0.5 0.75    1 <NA>
##   1       0    0    0    0  688    0
##   2       0    0    0 1763    0    0
##   3       0    0 1822    0    0    0
##   4       0 1861    0    0    0    0
##   5     778    0    0    0    0    0
##   <NA>    0    0    0    0    0  424
```

```r
# misrecognition of need for basic services
table(d1$q46c, useNA = "always") # frequencies old 
```

```
## 
##    1    2    3    4    5 <NA> 
##  299  806 1487 2326 1992  426
```

```r
table(d1$misrec_services, useNA = "always") # frequencies new
```

```
## 
##    0 0.25  0.5 0.75    1 <NA> 
## 1992 2326 1487  806  299  426
```

```r
table(d1$q46c,d1$misrec_services, useNA = "always") # compare
```

```
##       
##           0 0.25  0.5 0.75    1 <NA>
##   1       0    0    0    0  299    0
##   2       0    0    0  806    0    0
##   3       0    0 1487    0    0    0
##   4       0 2326    0    0    0    0
##   5    1992    0    0    0    0    0
##   <NA>    0    0    0    0    0  426
```

```r
# misrecognition of opinion 
table(d1$q46d, useNA = "always") # frequencies old 
```

```
## 
##    1    2    3    4    5 <NA> 
##  387  699 1081 1650 3126  393
```

```r
table(d1$misrec_opinion, useNA = "always") # frequencies new
```

```
## 
##    0 0.25  0.5 0.75    1 <NA> 
## 3126 1650 1081  699  387  393
```

```r
table(d1$q46d,d1$misrec_opinion, useNA = "always") # compare
```

```
##       
##           0 0.25  0.5 0.75    1 <NA>
##   1       0    0    0    0  387    0
##   2       0    0    0  699    0    0
##   3       0    0 1081    0    0    0
##   4       0 1650    0    0    0    0
##   5    3126    0    0    0    0    0
##   <NA>    0    0    0    0    0  393
```

```r
# -> looks all good :) 


# create an index, where values in one dimension can cause a higher overall value -- from Steiner et al. 

d1 <- d1 %>%
  mutate(
    misrecog_index = (  # index of choice 
      misrec_economic^2 +
      misrec_work^2 +
      misrec_services^2 +
      misrec_opinion^2
    ) / 4,
    misrecog_meanindex = ( # just for comparison reasons 
      misrec_economic +
      misrec_work +
      misrec_services +
      misrec_opinion
    ) / 4
  )
```


$$
I_i = \frac{
\mathrm{Economic}_i^2 +
\mathrm{Work}_i^2 +
\mathrm{Services}_i^2 +
\mathrm{Opinion}_i^2
}{4}
$$




```r
################################################################
# Potential Sociodemographic Confounders for Regression Models
################################################################


#----------------
# Gender: d1
#----------------
unique(data$d1) # get an overview 
```

```
## <labelled<double>[2]>: Geschlecht
## [1] 1 2
## 
## Labels:
##  value                           label
##    -99                    keine Angabe
##    -98                     weiss nicht
##    -97                 trifft nicht zu
##    -96                           Split
##    -95              nicht teilgenommen
##    -94      nicht in Auswahlgesamtheit
##    -93           Interview abgebrochen
##    -92                 Fehler in Daten
##    -91                           Modus
##    -86            nicht wahlberechtigt
##    -85                   nicht waehlen
##    -84 keine Erst-/Zweitstimme abgeben
##    -83               ungueltig waehlen
##    -82     keine andere Partei waehlen
##    -81          noch nicht entschieden
##    -73               Mehrfachnennungen
##    -72            nicht einzuschaetzen
##    -71                   nicht bekannt
##      1                       maennlich
##      2                        weiblich
##      3               non-binaer/divers
##  NA(a)                    keine Angabe
##  NA(b)                     weiss nicht
##  NA(c)                 trifft nicht zu
##  NA(d)                           Split
##  NA(e)              nicht teilgenommen
##  NA(f)      nicht in Auswahlgesamtheit
##  NA(g)           Interview abgebrochen
##  NA(h)                 Fehler in Daten
##  NA(i)                           Modus
##  NA(j)            nicht wahlberechtigt
##  NA(k)                   nicht waehlen
##  NA(l) keine Erst-/Zweitstimme abgeben
##  NA(m)               ungueltig waehlen
##  NA(n)     keine andere Partei waehlen
##  NA(o)          noch nicht entschieden
##  NA(p)            nicht einzuschaetzen
##  NA(q)                   nicht bekannt
##  NA(r)               Mehrfachnennungen
```

```r
table(data$d1, useNA = "always") # frequencies 
```

```
## 
##    1    2 <NA> 
## 3740 3596    0
```

```r
attr(data$d1, "labels") # check labels
```

```
##                    keine Angabe                     weiss nicht 
##                             -99                             -98 
##                 trifft nicht zu                           Split 
##                             -97                             -96 
##              nicht teilgenommen      nicht in Auswahlgesamtheit 
##                             -95                             -94 
##           Interview abgebrochen                 Fehler in Daten 
##                             -93                             -92 
##                           Modus            nicht wahlberechtigt 
##                             -91                             -86 
##                   nicht waehlen keine Erst-/Zweitstimme abgeben 
##                             -85                             -84 
##               ungueltig waehlen     keine andere Partei waehlen 
##                             -83                             -82 
##          noch nicht entschieden               Mehrfachnennungen 
##                             -81                             -73 
##            nicht einzuschaetzen                   nicht bekannt 
##                             -72                             -71 
##                       maennlich                        weiblich 
##                               1                               2 
##               non-binaer/divers                    keine Angabe 
##                               3                              NA 
##                     weiss nicht                 trifft nicht zu 
##                              NA                              NA 
##                           Split              nicht teilgenommen 
##                              NA                              NA 
##      nicht in Auswahlgesamtheit           Interview abgebrochen 
##                              NA                              NA 
##                 Fehler in Daten                           Modus 
##                              NA                              NA 
##            nicht wahlberechtigt                   nicht waehlen 
##                              NA                              NA 
## keine Erst-/Zweitstimme abgeben               ungueltig waehlen 
##                              NA                              NA 
##     keine andere Partei waehlen          noch nicht entschieden 
##                              NA                              NA 
##            nicht einzuschaetzen                   nicht bekannt 
##                              NA                              NA 
##               Mehrfachnennungen 
##                              NA
```

```r
# males = 1, females = 2, others = 3 // but others are randomized to male and female 

# create new variable: female
d1 <- d1 %>%
  mutate(
    female = case_when(
      d1 == 1 ~ 0, # males
      d1 == 2 ~ 1, # females 
      TRUE ~ NA_real_ ) )

#check if it worked 
table(d1$female, useNA = "always") #looks all good 
```

```
## 
##    0    1 <NA> 
## 3740 3596    0
```

```r
#----------------------------
# Education (school): d7
#----------------------------
unique(data$d7) # get an overview 
```

```
## <labelled<double>[10]>: Bildung: Schule
##  [1]   4 -99   5   3   2   6   1   9 -93 -73
## 
## Labels:
##  value
##    -99
##    -98
##    -97
##    -96
##    -95
##    -94
##    -93
##    -92
##    -91
##    -86
##    -85
##    -84
##    -83
##    -82
##    -81
##    -73
##    -72
##    -71
##      1
##      2
##      3
##      4
##      5
##      6
##      9
##  NA(a)
##  NA(b)
##  NA(c)
##  NA(d)
##  NA(e)
##  NA(f)
##  NA(g)
##  NA(h)
##  NA(i)
##  NA(j)
##  NA(k)
##  NA(l)
##  NA(m)
##  NA(n)
##  NA(o)
##  NA(p)
##  NA(q)
##  NA(r)
##                                                                                                        label
##                                                                                                 keine Angabe
##                                                                                                  weiss nicht
##                                                                                              trifft nicht zu
##                                                                                                        Split
##                                                                                           nicht teilgenommen
##                                                                                   nicht in Auswahlgesamtheit
##                                                                                        Interview abgebrochen
##                                                                                              Fehler in Daten
##                                                                                                        Modus
##                                                                                         nicht wahlberechtigt
##                                                                                                nicht waehlen
##                                                                              keine Erst-/Zweitstimme abgeben
##                                                                                            ungueltig waehlen
##                                                                                  keine andere Partei waehlen
##                                                                                       noch nicht entschieden
##                                                                                            Mehrfachnennungen
##                                                                                         nicht einzuschaetzen
##                                                                                                nicht bekannt
##                                                                                Schule beendet ohne Abschluss
##         Hauptschulabschluss, Volksschulabschluss, Abschluss der Polytechnischen Oberschule 8. oder 9. Klasse
##  Realschulabschluss, Mittlere Reife, Fachschulreife oder Abschluss der Polytechnischen Oberschule 10. Klasse
##                                                     Fachhochschulreife (Abschluss einer Fachoberschule etc.)
##                                  Abitur bzw. erweiterte Oberschule mit Abschluss 12. Klasse (Hochschulreife)
##                                                                             anderen Schulabschluss, und zwar
##                                                                                         bin noch Schueler/in
##                                                                                                 keine Angabe
##                                                                                                  weiss nicht
##                                                                                              trifft nicht zu
##                                                                                                        Split
##                                                                                           nicht teilgenommen
##                                                                                   nicht in Auswahlgesamtheit
##                                                                                        Interview abgebrochen
##                                                                                              Fehler in Daten
##                                                                                                        Modus
##                                                                                         nicht wahlberechtigt
##                                                                                                nicht waehlen
##                                                                              keine Erst-/Zweitstimme abgeben
##                                                                                            ungueltig waehlen
##                                                                                  keine andere Partei waehlen
##                                                                                       noch nicht entschieden
##                                                                                         nicht einzuschaetzen
##                                                                                                nicht bekannt
##                                                                                            Mehrfachnennungen
```

```r
table(data$d7, useNA = "always") # frequencies
```

```
## 
##  -99  -93  -73    1    2    3    4    5    6    9 <NA> 
##   46  139   51   49  877 2248  966 2801   33  126    0
```

```r
# recode missing values 
data_clean$d7[data_clean$d7 == -99] <- tagged_na("a")
data_clean$d7[data_clean$d7 == -93] <- tagged_na("g")
data_clean$d7[data_clean$d7 == -73] <- tagged_na("r")

table(data$d7, useNA = "always") # frequencies old 
```

```
## 
##  -99  -93  -73    1    2    3    4    5    6    9 <NA> 
##   46  139   51   49  877 2248  966 2801   33  126    0
```

```r
table(data_clean$d7, useNA = "always") # frequencies new #looks good 
```

```
## 
##    1    2    3    4    5    6    9 <NA> 
##   49  877 2248  966 2801   33  126  236
```

```r
# create a new variable: education
d1 <- d1 %>%
  mutate(
    education = case_when(
      d7 %in% c(1, 2) ~ "Low",
      d7 == 3 ~ "Medium",
      d7 %in% c(4, 5) ~ "High",
      TRUE ~ NA_character_  
      ),
    education = factor(
      education,
      levels = c("Low", "Medium", "High") ))

table(d1$education, useNA = "always") #looks all good
```

```
## 
##    Low Medium   High   <NA> 
##    926   2248   3767    395
```

```r
#---------------------
# Age: d2a
#---------------------
sort(unique(data$d2a)) # get an overview 
```

```
##  [1] "-99 keine Angabe"  "1935 oder frueher" "1936"             
##  [4] "1937"              "1938"              "1939"             
##  [7] "1940"              "1941"              "1942"             
## [10] "1943"              "1944"              "1945"             
## [13] "1946"              "1947"              "1948"             
## [16] "1949"              "1950"              "1951"             
## [19] "1952"              "1953"              "1954"             
## [22] "1955"              "1956"              "1957"             
## [25] "1958"              "1959"              "1960"             
## [28] "1961"              "1962"              "1963"             
## [31] "1964"              "1965"              "1966"             
## [34] "1967"              "1968"              "1969"             
## [37] "1970"              "1971"              "1972"             
## [40] "1973"              "1974"              "1975"             
## [43] "1976"              "1977"              "1978"             
## [46] "1979"              "1980"              "1981"             
## [49] "1982"              "1983"              "1984"             
## [52] "1985"              "1986"              "1987"             
## [55] "1988"              "1989"              "1990"             
## [58] "1991"              "1992"              "1993"             
## [61] "1994"              "1995"              "1996"             
## [64] "1997"              "1998"              "1999"             
## [67] "2000"              "2001"              "2002"             
## [70] "2003"              "2004"              "2005"             
## [73] "2006"              "2007"              "2008"             
## [76] "2009"
```

```r
table(data$d2a, useNA = "always") # frequencies 
```

```
## 
##  -99 keine Angabe 1935 oder frueher              1936              1937 
##                73                45                18                38 
##              1938              1939              1940              1941 
##                42                45                62                77 
##              1942              1943              1944              1945 
##                73                85                75                42 
##              1946              1947              1948              1949 
##                45                54                80                78 
##              1950              1951              1952              1953 
##               102               120               126               132 
##              1954              1955              1956              1957 
##               127               147               115               163 
##              1958              1959              1960              1961 
##               142               156               148               165 
##              1962              1963              1964              1965 
##               153               156               164               187 
##              1966              1967              1968              1969 
##               150               152               142               133 
##              1970              1971              1972              1973 
##               134               115                97                94 
##              1974              1975              1976              1977 
##                96               120                94               100 
##              1978              1979              1980              1981 
##               109               106               104               113 
##              1982              1983              1984              1985 
##               102                83                86               104 
##              1986              1987              1988              1989 
##                86               103               109                95 
##              1990              1991              1992              1993 
##                99                79                89                86 
##              1994              1995              1996              1997 
##                78                88                89                80 
##              1998              1999              2000              2001 
##                90                79                78                74 
##              2002              2003              2004              2005 
##                65                69                64                70 
##              2006              2007              2008              2009 
##                57                63                66                11 
##              <NA> 
##                 0
```

```r
# recoding missing values and creating a new variable: age
class(data$d2)
```

```
## Warning: Unknown or uninitialised column: `d2`.
```

```
## [1] "NULL"
```

```r
d1 <- d1 %>% 
  mutate(
    age = case_when(
      d2a == "1935 oder frueher" ~ 90,  
      TRUE ~ 2025 - as.numeric(d2a) ) ) 
```

```
## Warning: There was 1 warning in `mutate()`.
## ℹ In argument: `age = case_when(d2a == "1935 oder frueher" ~ 90, TRUE ~ 2025 -
##   as.numeric(d2a))`.
## Caused by warning:
## ! NAs durch Umwandlung erzeugt
```

```r
# check if it worked      
sort(unique(d1$age), na.last = TRUE)
```

```
##  [1] 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40
## [26] 41 42 43 44 45 46 47 48 49 50 51 52 53 54 55 56 57 58 59 60 61 62 63 64 65
## [51] 66 67 68 69 70 71 72 73 74 75 76 77 78 79 80 81 82 83 84 85 86 87 88 89 90
## [76] NA
```

```r
table(d1$age, useNA = "always") # looks good, all "-99 keine Angabe" are now coded as NAs
```

```
## 
##   16   17   18   19   20   21   22   23   24   25   26   27   28   29   30   31 
##   11   66   63   57   70   64   69   65   74   78   79   90   80   89   88   78 
##   32   33   34   35   36   37   38   39   40   41   42   43   44   45   46   47 
##   86   89   79   99   95  109  103   86  104   86   83  102  113  104  106  109 
##   48   49   50   51   52   53   54   55   56   57   58   59   60   61   62   63 
##  100   94  120   96   94   97  115  134  133  142  152  150  187  164  156  153 
##   64   65   66   67   68   69   70   71   72   73   74   75   76   77   78   79 
##  165  148  156  142  163  115  147  127  132  126  120  102   78   80   54   45 
##   80   81   82   83   84   85   86   87   88   89   90 <NA> 
##   42   75   85   73   77   62   45   42   38   18   45   73
```

```r
# create another age variable by groups
# code into groups
# 0 = up to 34
# 1 = 35 to 49
# 2 = 50 to 64
# 3 = 65 and older 

# create age_group (for robustness checks)
d1 <- d1 %>%
  mutate(
    age_group = case_when(
      age >= 16 & age <= 29 ~ "16-29",
      age >= 30 & age <= 44 ~ "30-44",
      age >= 45 & age <= 59 ~ "45-59",
      age >= 60 ~ "60+",
      TRUE ~ NA_character_ ),
    age_group = factor(
      age_group,
      levels = c("16-29", "30-44", "45-59", "60+") ) )

table(d1$age_group, useNA = "always") #looks all good 
```

```
## 
## 16-29 30-44 45-59   60+  <NA> 
##   955  1400  1746  3162    73
```

```r
#probably are going to change the groups again though 

#check again 
sum(!is.na(d1$age))
```

```
## [1] 7263
```

```r
sum(!is.na(d1$age_group))
```

```
## [1] 7263
```

```r
identical(is.na(d1$age), is.na(d1$age_group))
```

```
## [1] TRUE
```

```r
#------------------------------------------
# Place of residence rural vs. city : wum6
#------------------------------------------
sort(unique(data$wum6)) # get an overview 
```

```
## <labelled<double>[8]>: Wohnort: Stadt-Land
## [1] -99 -93 -73   1   2   3   4   5
## 
## Labels:
##  value                                                label
##    -99                                         keine Angabe
##    -98                                          weiss nicht
##    -97                                      trifft nicht zu
##    -96                                                Split
##    -95                                   nicht teilgenommen
##    -94                           nicht in Auswahlgesamtheit
##    -93                                Interview abgebrochen
##    -92                                      Fehler in Daten
##    -91                                                Modus
##    -86                                 nicht wahlberechtigt
##    -85                                        nicht waehlen
##    -84                      keine Erst-/Zweitstimme abgeben
##    -83                                    ungueltig waehlen
##    -82                          keine andere Partei waehlen
##    -81                               noch nicht entschieden
##    -73                                    Mehrfachnennungen
##    -72                                 nicht einzuschaetzen
##    -71                                        nicht bekannt
##      1                                           Grossstadt
##      2                    Rand oder Vorort einer Grossstadt
##      3                              Mittel- oder Kleinstadt
##      4                                     laendliches Dorf
##      5 Einzelgehoeft oder alleinstehendes Haus auf dem Land
##  NA(a)                                         keine Angabe
##  NA(b)                                          weiss nicht
##  NA(c)                                      trifft nicht zu
##  NA(d)                                                Split
##  NA(e)                                   nicht teilgenommen
##  NA(f)                           nicht in Auswahlgesamtheit
##  NA(g)                                Interview abgebrochen
##  NA(h)                                      Fehler in Daten
##  NA(i)                                                Modus
##  NA(j)                                 nicht wahlberechtigt
##  NA(k)                                        nicht waehlen
##  NA(l)                      keine Erst-/Zweitstimme abgeben
##  NA(m)                                    ungueltig waehlen
##  NA(n)                          keine andere Partei waehlen
##  NA(o)                               noch nicht entschieden
##  NA(p)                                 nicht einzuschaetzen
##  NA(q)                                        nicht bekannt
##  NA(r)                                    Mehrfachnennungen
```

```r
table(data$wum6, useNA = "always") # frequencies 
```

```
## 
##  -99  -93  -73    1    2    3    4    5 <NA> 
##   53  177    4 1512 1022 2325 2154   89    0
```

```r
# recode missing values 
data_clean$wum6[data_clean$wum6 == -99] <- tagged_na("a")
data_clean$wum6[data_clean$wum6 == -93] <- tagged_na("g")
data_clean$wum6[data_clean$wum6 == -73] <- tagged_na("r")

table(data_clean$wum6, useNA = "always") #check if it worked
```

```
## 
##    1    2    3    4    5 <NA> 
## 1512 1022 2325 2154   89  234
```

```r
# create a new variable (according to Steiner et. al)
d1$wum6 <- data_clean$wum6 # add cleaned variable wum6 to d1

d1 <- d1 %>%
  mutate(
    rural = case_when(
      wum6 %in% c(4, 5) ~ 1, # rural citizens
      wum6 %in% c(1, 2, 3) ~ 0, # other
      TRUE ~ NA_real_ ) )
# check if it worked
table(d1$wum6, useNA = "always") 
```

```
## 
##    1    2    3    4    5 <NA> 
## 1512 1022 2325 2154   89  234
```

```r
table(d1$rural, useNA = "always") 
```

```
## 
##    0    1 <NA> 
## 4859 2243  234
```

```r
# check again 
sum(!is.na(d1$wum6))
```

```
## [1] 7102
```

```r
sum(!is.na(d1$rural))
```

```
## [1] 7102
```

```r
identical(is.na(d1$wum6), is.na(d1$rural))
```

```
## [1] TRUE
```

```r
#---------------
# East-West 
#---------------

unique(data$ostwest2)
```

```
## <labelled<double>[2]>: Ost/West (genaue Zuordnung von Berlin zu Ost- und Westdeutschland)
## [1] 1 0
## 
## Labels:
##  value                           label
##    -99                    keine Angabe
##    -98                     weiss nicht
##    -97                 trifft nicht zu
##    -96                           Split
##    -95              nicht teilgenommen
##    -94      nicht in Auswahlgesamtheit
##    -93           Interview abgebrochen
##    -92                 Fehler in Daten
##    -91                           Modus
##    -86            nicht wahlberechtigt
##    -85                   nicht waehlen
##    -84 keine Erst-/Zweitstimme abgeben
##    -83               ungueltig waehlen
##    -82     keine andere Partei waehlen
##    -81          noch nicht entschieden
##    -72            nicht einzuschaetzen
##    -71                   nicht bekannt
##      0                  Ostdeutschland
##      1                 Westdeutschland
##      2                             Ost
##  NA(a)                    keine Angabe
##  NA(b)                     weiss nicht
##  NA(c)                 trifft nicht zu
##  NA(d)                           Split
##  NA(e)              nicht teilgenommen
##  NA(f)      nicht in Auswahlgesamtheit
##  NA(g)           Interview abgebrochen
##  NA(h)                 Fehler in Daten
##  NA(i)                           Modus
##  NA(j)            nicht wahlberechtigt
##  NA(k)                   nicht waehlen
##  NA(l) keine Erst-/Zweitstimme abgeben
##  NA(m)               ungueltig waehlen
##  NA(n)     keine andere Partei waehlen
##  NA(o)          noch nicht entschieden
##  NA(p)            nicht einzuschaetzen
##  NA(q)                   nicht bekannt
##  NA(r)               Mehrfachnennungen
```

```r
table(data$ostwest2, useNA = "always")
```

```
## 
##    0    1 <NA> 
## 2473 4863    0
```

```r
attr(data$ostwest2, "labels") # Ost = 0, West = 1 
```

```
##                    keine Angabe                     weiss nicht 
##                             -99                             -98 
##                 trifft nicht zu                           Split 
##                             -97                             -96 
##              nicht teilgenommen      nicht in Auswahlgesamtheit 
##                             -95                             -94 
##           Interview abgebrochen                 Fehler in Daten 
##                             -93                             -92 
##                           Modus            nicht wahlberechtigt 
##                             -91                             -86 
##                   nicht waehlen keine Erst-/Zweitstimme abgeben 
##                             -85                             -84 
##               ungueltig waehlen     keine andere Partei waehlen 
##                             -83                             -82 
##          noch nicht entschieden            nicht einzuschaetzen 
##                             -81                             -72 
##                   nicht bekannt                  Ostdeutschland 
##                             -71                               0 
##                 Westdeutschland                             Ost 
##                               1                               2 
##                    keine Angabe                     weiss nicht 
##                              NA                              NA 
##                 trifft nicht zu                           Split 
##                              NA                              NA 
##              nicht teilgenommen      nicht in Auswahlgesamtheit 
##                              NA                              NA 
##           Interview abgebrochen                 Fehler in Daten 
##                              NA                              NA 
##                           Modus            nicht wahlberechtigt 
##                              NA                              NA 
##                   nicht waehlen keine Erst-/Zweitstimme abgeben 
##                              NA                              NA 
##               ungueltig waehlen     keine andere Partei waehlen 
##                              NA                              NA 
##          noch nicht entschieden            nicht einzuschaetzen 
##                              NA                              NA 
##                   nicht bekannt               Mehrfachnennungen 
##                              NA                              NA
```

```r
table(d1$ostwest2, useNA = "always")
```

```
## 
##    0    1 <NA> 
## 2473 4863    0
```

```r
attr(d1$ostwest2, "labels") # Ost = 0, West = 1 
```

```
##                    keine Angabe                     weiss nicht 
##                             -99                             -98 
##                 trifft nicht zu                           Split 
##                             -97                             -96 
##              nicht teilgenommen      nicht in Auswahlgesamtheit 
##                             -95                             -94 
##           Interview abgebrochen                 Fehler in Daten 
##                             -93                             -92 
##                           Modus            nicht wahlberechtigt 
##                             -91                             -86 
##                   nicht waehlen keine Erst-/Zweitstimme abgeben 
##                             -85                             -84 
##               ungueltig waehlen     keine andere Partei waehlen 
##                             -83                             -82 
##          noch nicht entschieden            nicht einzuschaetzen 
##                             -81                             -72 
##                   nicht bekannt                  Ostdeutschland 
##                             -71                               0 
##                 Westdeutschland                             Ost 
##                               1                               2 
##                    keine Angabe                     weiss nicht 
##                              NA                              NA 
##                 trifft nicht zu                           Split 
##                              NA                              NA 
##              nicht teilgenommen      nicht in Auswahlgesamtheit 
##                              NA                              NA 
##           Interview abgebrochen                 Fehler in Daten 
##                              NA                              NA 
##                           Modus            nicht wahlberechtigt 
##                              NA                              NA 
##                   nicht waehlen keine Erst-/Zweitstimme abgeben 
##                              NA                              NA 
##               ungueltig waehlen     keine andere Partei waehlen 
##                              NA                              NA 
##          noch nicht entschieden            nicht einzuschaetzen 
##                              NA                              NA 
##                   nicht bekannt               Mehrfachnennungen 
##                              NA                              NA
```

```r
# create new variable: east (so that east= 1 and west = 0 )
d1 <- d1 %>%
  mutate(
    east = case_when(
      ostwest2 == 0 ~ 1, # east
      ostwest2 == 1 ~ 0,# west 
      TRUE ~ NA_real_  ) )

#check if it worked 
table(d1$east, useNA = "always")
```

```
## 
##    0    1 <NA> 
## 4863 2473    0
```

```r
#------------------------------------------
# Ideology/ Left-right-self placement: q37
#------------------------------------------
sort(unique(data$q37)) # get an overview 
```

```
## <labelled<double>[15]>: Links-Rechts-Einstufung: Ego
##  [1] -99 -98 -97 -92   1   2   3   4   5   6   7   8   9  10  11
## 
## Labels:
##  value                           label
##    -99                    keine Angabe
##    -98                     weiss nicht
##    -97                 trifft nicht zu
##    -96                           Split
##    -95              nicht teilgenommen
##    -94      nicht in Auswahlgesamtheit
##    -93           Interview abgebrochen
##    -92                 Fehler in Daten
##    -91                           Modus
##    -86            nicht wahlberechtigt
##    -85                   nicht waehlen
##    -84 keine Erst-/Zweitstimme abgeben
##    -83               ungueltig waehlen
##    -82     keine andere Partei waehlen
##    -81          noch nicht entschieden
##    -73               Mehrfachnennungen
##    -72            nicht einzuschaetzen
##    -71                   nicht bekannt
##      1                         1 links
##      2                               2
##      3                               3
##      4                               4
##      5                               5
##      6       6 weder links noch rechts
##      7                               7
##      8                               8
##      9                               9
##     10                              10
##     11                       11 rechts
##  NA(a)                    keine Angabe
##  NA(b)                     weiss nicht
##  NA(c)                 trifft nicht zu
##  NA(d)                           Split
##  NA(e)              nicht teilgenommen
##  NA(f)      nicht in Auswahlgesamtheit
##  NA(g)           Interview abgebrochen
##  NA(h)                 Fehler in Daten
##  NA(i)                           Modus
##  NA(j)            nicht wahlberechtigt
##  NA(k)                   nicht waehlen
##  NA(l) keine Erst-/Zweitstimme abgeben
##  NA(m)               ungueltig waehlen
##  NA(n)     keine andere Partei waehlen
##  NA(o)          noch nicht entschieden
##  NA(p)            nicht einzuschaetzen
##  NA(q)                   nicht bekannt
##  NA(r)               Mehrfachnennungen
```

```r
table(data$q37, useNA = "always") # frequencies 
```

```
## 
##  -99  -98  -97  -92    1    2    3    4    5    6    7    8    9   10   11 <NA> 
##   93  133  128    1  260  374  729  666  682 2619  751  543  212   80   65    0
```

```r
# recode missing values 
data_clean$q37[data_clean$q37 == -99] <- tagged_na("a")
data_clean$q37[data_clean$q37 == -98] <- tagged_na("b")
data_clean$q37[data_clean$q37 == -97] <- tagged_na("c")
data_clean$q37[data_clean$q37 == -92] <- tagged_na("h")

# check again 
table(data$q37, useNA = "always") # frequencies old 
```

```
## 
##  -99  -98  -97  -92    1    2    3    4    5    6    7    8    9   10   11 <NA> 
##   93  133  128    1  260  374  729  666  682 2619  751  543  212   80   65    0
```

```r
table(data_clean$q37, useNA = "always") # frequencies new 
```

```
## 
##    1    2    3    4    5    6    7    8    9   10   11 <NA> 
##  260  374  729  666  682 2619  751  543  212   80   65  355
```

```r
d1$q37 <- data_clean$q37 # add cleaned variable q37 to d1
table(d1$q37, useNA = "always") #check if it worked
```

```
## 
##    1    2    3    4    5    6    7    8    9   10   11 <NA> 
##  260  374  729  666  682 2619  751  543  212   80   65  355
```

```r
# create a new variable: ideology 
d1 <- d1 %>%
  mutate(ideology = q37-1) #re-code scale from 0 to 10 for better interpretation 

# check if it worked 
table(d1$ideology, useNA = "always")
```

```
## 
##    0    1    2    3    4    5    6    7    8    9   10 <NA> 
##  260  374  729  666  682 2619  751  543  212   80   65  355
```

```r
# just for robustness: create a new variable that measures if a person identifies as right-of-center
d1 <- d1 %>%
  mutate(
    right_ideology = case_when(
      ideology >= 6 & ideology <= 10 ~ 1,
      ideology >= 0 & ideology <= 5 ~ 0,
      TRUE ~ NA_real_ ))

# check if it worked 
table(d1$right_ideology, useNA = "always")
```

```
## 
##    0    1 <NA> 
## 5330 1651  355
```

```r
# check again 
sum(!is.na(d1$ideology))
```

```
## [1] 6981
```

```r
sum(!is.na(d1$right_ideology))
```

```
## [1] 6981
```

```r
identical(is.na(d1$ideology), is.na(d1$right_ideology))
```

```
## [1] TRUE
```

```r
#-----------------------------------------------------------------------------

#---------------------------
# Social class, self : d38 
#---------------------------
sort(unique(data$d38)) # get an overview 
```

```
## <labelled<double>[9]>: Schichtzugehoerigkeit: subjektiv, eigene
## [1] -99 -93 -73   1   2   3   4   5   6
## 
## Labels:
##  value                           label
##    -99                    keine Angabe
##    -98                     weiss nicht
##    -97                 trifft nicht zu
##    -96                           Split
##    -95              nicht teilgenommen
##    -94      nicht in Auswahlgesamtheit
##    -93           Interview abgebrochen
##    -92                 Fehler in Daten
##    -91                           Modus
##    -86            nicht wahlberechtigt
##    -85                   nicht waehlen
##    -84 keine Erst-/Zweitstimme abgeben
##    -83               ungueltig waehlen
##    -82     keine andere Partei waehlen
##    -81          noch nicht entschieden
##    -73               Mehrfachnennungen
##    -72            nicht einzuschaetzen
##    -71                   nicht bekannt
##      1                    Unterschicht
##      2                 Arbeiterschicht
##      3            untere Mittelschicht
##      4          mittlere Mittelschicht
##      5             obere Mittelschicht
##      6                     Oberschicht
##  NA(a)                    keine Angabe
##  NA(b)                     weiss nicht
##  NA(c)                 trifft nicht zu
##  NA(d)                           Split
##  NA(e)              nicht teilgenommen
##  NA(f)      nicht in Auswahlgesamtheit
##  NA(g)           Interview abgebrochen
##  NA(h)                 Fehler in Daten
##  NA(i)                           Modus
##  NA(j)            nicht wahlberechtigt
##  NA(k)                   nicht waehlen
##  NA(l) keine Erst-/Zweitstimme abgeben
##  NA(m)               ungueltig waehlen
##  NA(n)     keine andere Partei waehlen
##  NA(o)          noch nicht entschieden
##  NA(p)            nicht einzuschaetzen
##  NA(q)                   nicht bekannt
##  NA(r)               Mehrfachnennungen
```

```r
table(data$d38, useNA = "always") # frequencies 
```

```
## 
##  -99  -93  -73    1    2    3    4    5    6 <NA> 
##  154  159    6  140 1006 1505 3000 1269   97    0
```

```r
# recode missing values
data_clean$d38[data_clean$d38 == -99] <- tagged_na("a")
data_clean$d38[data_clean$d38 == -93] <- tagged_na("g")
data_clean$d38[data_clean$d38 == -73] <- tagged_na("r")

table(data_clean$d38, useNA = "always")
```

```
## 
##    1    2    3    4    5    6 <NA> 
##  140 1006 1505 3000 1269   97  319
```

```r
d1$d38 <- data_clean$d38 # add cleaned variable to d1

# create new variable: social_class
# group order just for first impressions, not perfectly justified
d1 <- d1 %>%
  mutate(
    social_class = case_when(
      d38 %in% c(1, 2) ~ "Lower Classes",
      d38 %in% c(3, 4) ~ "Middle Classes",
      d38 %in% c(5, 6) ~ "Upper Classes",
      TRUE ~ NA_character_
      ),
    social_class = factor(
      social_class,
      levels = c(
        "Middle Classes",
        "Lower Classes",
        "Upper Classes"  ) ) )

# check if it worked
table(d1$d38, useNA = "always") #old
```

```
## 
##    1    2    3    4    5    6 <NA> 
##  140 1006 1505 3000 1269   97  319
```

```r
table(d1$social_class, useNA = "always") #new # looks good
```

```
## 
## Middle Classes  Lower Classes  Upper Classes           <NA> 
##           4505           1146           1366            319
```

```r
#-----------------------------------------
# subjective social status: d70 
#-----------------------------------------
sort(unique(data$d70)) # get an overview 
```

```
## <labelled<double>[14]>: Sozialer Status: subjektiv
##  [1] -99 -93 -73   1   2   3   4   5   6   7   8   9  10  11
## 
## Labels:
##  value                           label
##    -99                    keine Angabe
##    -98                     weiss nicht
##    -97                 trifft nicht zu
##    -96                           Split
##    -95              nicht teilgenommen
##    -94      nicht in Auswahlgesamtheit
##    -93           Interview abgebrochen
##    -92                 Fehler in Daten
##    -91                           Modus
##    -86            nicht wahlberechtigt
##    -85                   nicht waehlen
##    -84 keine Erst-/Zweitstimme abgeben
##    -83               ungueltig waehlen
##    -82     keine andere Partei waehlen
##    -81          noch nicht entschieden
##    -73               Mehrfachnennungen
##    -72            nicht einzuschaetzen
##    -71                   nicht bekannt
##      1                    1 ganz unten
##      2                               2
##      3                               3
##      4                               4
##      5                               5
##      6                               6
##      7                               7
##      8                               8
##      9                               9
##     10                              10
##     11                    11 ganz oben
##  NA(a)                    keine Angabe
##  NA(b)                     weiss nicht
##  NA(c)                 trifft nicht zu
##  NA(d)                           Split
##  NA(e)              nicht teilgenommen
##  NA(f)      nicht in Auswahlgesamtheit
##  NA(g)           Interview abgebrochen
##  NA(h)                 Fehler in Daten
##  NA(i)                           Modus
##  NA(j)            nicht wahlberechtigt
##  NA(k)                   nicht waehlen
##  NA(l) keine Erst-/Zweitstimme abgeben
##  NA(m)               ungueltig waehlen
##  NA(n)     keine andere Partei waehlen
##  NA(o)          noch nicht entschieden
##  NA(p)            nicht einzuschaetzen
##  NA(q)                   nicht bekannt
##  NA(r)               Mehrfachnennungen
```

```r
table(data$d70, useNA = "always") # frequencies 
```

```
## 
##  -99  -93  -73    1    2    3    4    5    6    7    8    9   10   11 <NA> 
##  177  165    4   61   77  267  517  922 1517 1530 1393  562  103   41    0
```

```r
# recode missing values 
data_clean$d70[data_clean$d70 == -99] <- tagged_na("a")
data_clean$d70[data_clean$d70 == -93] <- tagged_na("g")
data_clean$d70[data_clean$d70 == -73] <- tagged_na("r")

# check if it worked 
table(data_clean$d70, useNA = "always")
```

```
## 
##    1    2    3    4    5    6    7    8    9   10   11 <NA> 
##   61   77  267  517  922 1517 1530 1393  562  103   41  346
```

```r
d1$d70 <- data_clean$d70 # add cleaned variable to d1

# create new variable: subjective status
d1 <- d1 %>%
  mutate(
    subj_status = d70 -1)

#check if it worked
table(d1$subj_status, useNA = "always") #looks good 
```

```
## 
##    0    1    2    3    4    5    6    7    8    9   10 <NA> 
##   61   77  267  517  922 1517 1530 1393  562  103   41  346
```

```r
#--------------------------------
# economic situation, self: q13
#--------------------------------
sort(unique(data$q13)) # get an overview 
```

```
## <labelled<double>[8]>: Wirtschaftliche Lage: aktuell, eigene
## [1] -99 -93 -73   1   2   3   4   5
## 
## Labels:
##  value                           label
##    -99                    keine Angabe
##    -98                     weiss nicht
##    -97                 trifft nicht zu
##    -96                           Split
##    -95              nicht teilgenommen
##    -94      nicht in Auswahlgesamtheit
##    -93           Interview abgebrochen
##    -92                 Fehler in Daten
##    -91                           Modus
##    -86            nicht wahlberechtigt
##    -85                   nicht waehlen
##    -84 keine Erst-/Zweitstimme abgeben
##    -83               ungueltig waehlen
##    -82     keine andere Partei waehlen
##    -81          noch nicht entschieden
##    -73               Mehrfachnennungen
##    -72            nicht einzuschaetzen
##    -71                   nicht bekannt
##      1                        sehr gut
##      2                             gut
##      3                     teils/teils
##      4                        schlecht
##      5                   sehr schlecht
##  NA(a)                    keine Angabe
##  NA(b)                     weiss nicht
##  NA(c)                 trifft nicht zu
##  NA(d)                           Split
##  NA(e)              nicht teilgenommen
##  NA(f)      nicht in Auswahlgesamtheit
##  NA(g)           Interview abgebrochen
##  NA(h)                 Fehler in Daten
##  NA(i)                           Modus
##  NA(j)            nicht wahlberechtigt
##  NA(k)                   nicht waehlen
##  NA(l) keine Erst-/Zweitstimme abgeben
##  NA(m)               ungueltig waehlen
##  NA(n)     keine andere Partei waehlen
##  NA(o)          noch nicht entschieden
##  NA(p)            nicht einzuschaetzen
##  NA(q)                   nicht bekannt
##  NA(r)               Mehrfachnennungen
```

```r
table(data$q13, useNA = "always") # frequencies 
```

```
## 
##  -99  -93  -73    1    2    3    4    5 <NA> 
##   33  137    1  823 3724 1908  603  107    0
```

```r
# recode missing values 
data_clean$q13[data_clean$q13 == -99] <- tagged_na("a")
data_clean$q13[data_clean$q13 == -93] <- tagged_na("g")
data_clean$q13[data_clean$q13 == -73] <- tagged_na("r")

#check if it worked
table(data_clean$q13, useNA = "always")
```

```
## 
##    1    2    3    4    5 <NA> 
##  823 3724 1908  603  107  171
```

```r
d1$q13 <- data_clean$q13 # add variable to d1
table(d1$q13, useNA =  "always")
```

```
## 
##    1    2    3    4    5 <NA> 
##  823 3724 1908  603  107  171
```

```r
# create new variable: economic situation
d1 <- d1 %>%
  mutate(
    econ_situ = (q13 - 1) / 4  ) #rescale from 0 to 1
# higher values indicate a worse economic situation 

table(d1$q13, d1$econ_situ, useNA = "always")
```

```
##       
##           0 0.25  0.5 0.75    1 <NA>
##   1     823    0    0    0    0    0
##   2       0 3724    0    0    0    0
##   3       0    0 1908    0    0    0
##   4       0    0    0  603    0    0
##   5       0    0    0    0  107    0
##   <NA>    0    0    0    0    0  171
```

```r
table(d1$econ_situ, useNA = "always")
```

```
## 
##    0 0.25  0.5 0.75    1 <NA> 
##  823 3724 1908  603  107  171
```

```r
#---------------------------
# political knowledge: q5
#---------------------------
sort(unique(data$q5)) # get an overview 
```

```
## <labelled<double>[6]>: Politisches Wissen: Erst/Zweitstimme
## [1] -99 -98 -73   1   2   3
## 
## Labels:
##  value                           label
##    -99                    keine Angabe
##    -98                     weiss nicht
##    -97                 trifft nicht zu
##    -96                           Split
##    -95              nicht teilgenommen
##    -94      nicht in Auswahlgesamtheit
##    -93           Interview abgebrochen
##    -92                 Fehler in Daten
##    -91                           Modus
##    -86            nicht wahlberechtigt
##    -85                   nicht waehlen
##    -84 keine Erst-/Zweitstimme abgeben
##    -83               ungueltig waehlen
##    -82     keine andere Partei waehlen
##    -81          noch nicht entschieden
##    -73               Mehrfachnennungen
##    -72            nicht einzuschaetzen
##    -71                   nicht bekannt
##      1                      Erststimme
##      2                     Zweitstimme
##      3       beide sind gleich wichtig
##  NA(a)                    keine Angabe
##  NA(b)                     weiss nicht
##  NA(c)                 trifft nicht zu
##  NA(d)                           Split
##  NA(e)              nicht teilgenommen
##  NA(f)      nicht in Auswahlgesamtheit
##  NA(g)           Interview abgebrochen
##  NA(h)                 Fehler in Daten
##  NA(i)                           Modus
##  NA(j)            nicht wahlberechtigt
##  NA(k)                   nicht waehlen
##  NA(l) keine Erst-/Zweitstimme abgeben
##  NA(m)               ungueltig waehlen
##  NA(n)     keine andere Partei waehlen
##  NA(o)          noch nicht entschieden
##  NA(p)            nicht einzuschaetzen
##  NA(q)                   nicht bekannt
##  NA(r)               Mehrfachnennungen
```

```r
table(data$q5, useNA = "always") # frequencies 
```

```
## 
##  -99  -98  -73    1    2    3 <NA> 
##   45  483    7 1122 4673 1006    0
```

```r
# recode missing values 
data_clean$q5[data_clean$q5 == -99] <- tagged_na("a")
data_clean$q5[data_clean$q5 == -73] <- tagged_na("r")
# -98 = in this case no missing, but coded as 0 

# check if it worked
table(data_clean$q5, useNA = "always") #looks good
```

```
## 
##  -98    1    2    3 <NA> 
##  483 1122 4673 1006   52
```

```r
d1$q5 <- d1$q5 # add to d1

d1 <- d1 %>%
  mutate(
    pol_knowledge = case_when(
      q5 == 2 ~ 1, # correct answer
      q5 %in% c(1, 3, -98) ~ 0, # false answer or "don't know" 
      TRUE ~ NA_real_ ))
table(d1$pol_knowledge, useNA = "always")
```

```
## 
##    0    1 <NA> 
## 2611 4673   52
```


Creating Data Set for Analysis 


```r
############ creating data set #############
##########################################

# create a reduced data set for analysis with all the variables and weights I want to keep 
analysis <- d1 %>%
  dplyr::select(
    afd_vote,
    misrec_economic, misrec_work, misrec_services, misrec_opinion, misrecog_index, misrecog_meanindex,
    female, age, age_group, education,
    east, rural,
    ideology, right_ideology,
    pol_knowledge,
    subj_status, social_class, econ_situ,
    w_ow, w_ipfges, lfdn ) 

# reduces analysis data set to observations with available weight -> 236 are excluded 
analysis_weights <- analysis %>%
  filter(!is.na(w_ipfges), w_ipfges > 0)

# data set with same N for all variables for regression analysis 
analysis_reg <- analysis_weights %>%
  tidyr::drop_na(
    afd_vote,
    misrec_economic,
    misrec_work,
    misrec_services,
    misrec_opinion,
    misrecog_index,
    misrecog_meanindex,
    female,
    age,
    education,
    east,
    rural )
```






## I. Descriptive Statistics 


1) Univariate Distribution of AfD vote choice 

```r
# get an overview 
table(data_clean$q114ba, useNA = "always") #distribution of all parties
```

```
## 
##    1    4    5    6    7  322  392  801 <NA> 
## 1842 1015  282 1119  751  857  348  200  922
```

```r
prop.table(table(d1$q114ba)) * 100 # frequencies all parties
```

```
## 
##         1         4         5         6         7       322       392       801 
## 28.718428 15.824758  4.396632 17.446211 11.708762 13.361397  5.425631  3.118179
```

```r
# N = 6414 without missings 
sum(!is.na(analysis$afd_vote)) 
```

```
## [1] 6414
```

```r
#---------------------------------------
# univariate distribution of AfD vote 
#---------------------------------------

# distribution AfD vs. others

table(analysis$afd_vote, useNA = "always") 
```

```
## 
##    0    1 <NA> 
## 5557  857  922
```

```r
proportions(table(analysis$afd_vote)) * 100 # unweighted
```

```
## 
##       0       1 
## 86.6386 13.3614
```

```r
proportions(                                # weighted
  xtabs(w_ipfges ~ afd_vote,     
        data = analysis_weights)) * 100  
```

```
## afd_vote
##        0        1 
## 85.63369 14.36631
```

```r
# table of frequencies #
vote_table <- analysis %>%
  filter(!is.na(afd_vote),
         !is.na(w_ipfges),
         w_ipfges > 0) %>%
  group_by(afd_vote) %>%
  summarise(
    N = n(),
    Weight = sum(w_ipfges),
    .groups = "drop"
) %>%
  mutate(
    Vote = ifelse(afd_vote == 1, "AfD", "Other parties"),
    Percentage = round(Weight / sum(Weight) * 100, 2)
 ) %>%
  dplyr::select(Vote, N, Percentage)
# Add total row
vote_table <- bind_rows(
  vote_table,
  tibble(
    Vote = "Total",
    N = sum(vote_table$N),
    Percentage = 100 ))
# produce table
knitr::kable(
  vote_table,
  col.names = c("Second-vote choice", "N", "Weighted (%)"),
  caption = "Distribution of second-vote choice")
```



Table: Distribution of second-vote choice

|Second-vote choice |    N| Weighted (%)|
|:------------------|----:|------------:|
|Other parties      | 5393|        85.63|
|AfD                |  830|        14.37|
|Total              | 6223|       100.00|

```r
# save the table 
library(stargazer)
stargazer(
  vote_table,
  type = "html",
  summary = FALSE,
  rownames = FALSE,
  title = "Distribution of Second-Vote Choice",
  column.labels = NULL,
  digits = 2,
  out = "vote_table.html")
```

```
## 
## <table style="text-align:center"><caption><strong>Distribution of Second-Vote Choice</strong></caption>
## <tr><td colspan="3" style="border-bottom: 1px solid black"></td></tr><tr><td style="text-align:left">Vote</td><td>N</td><td>Percentage</td></tr>
## <tr><td colspan="3" style="border-bottom: 1px solid black"></td></tr><tr><td style="text-align:left">Other parties</td><td>5393</td><td>85.63</td></tr>
## <tr><td style="text-align:left">AfD</td><td>830</td><td>14.37</td></tr>
## <tr><td style="text-align:left">Total</td><td>6223</td><td>100</td></tr>
## <tr><td colspan="3" style="border-bottom: 1px solid black"></td></tr></table>
```





```r
# create a plot: distribution of second votes 
ggplot(
  filter(vote_table, Vote != "Total") %>%
    mutate(Position = ifelse(Vote == "Other parties", 1, 1.45)),
  aes(x = Position, y = Percentage, fill = Vote)
) +
  geom_col(width = 0.2) +
  geom_text(
    aes(label = paste0(Percentage, "%")),
    vjust = -0.5
  ) +
  scale_fill_manual(values = c(
    "Other parties" = "#A9C8DF",
    "AfD" = "#245A81"
  )) +
  scale_x_continuous(
    breaks = c(1, 1.45),
    labels = c("Other parties", "AfD"),
    limits = c(0.7, 1.75)
  ) +
  scale_y_continuous(limits = c(0, 100)) +
  labs(
    title = "",
    x = NULL,
    y = "Weighted percentage (%)"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(hjust = 0.5, size = 11),
    legend.position = "none"
  )
```

<img src="master_thesis_files/figure-html/plot of distributions of second votes AfD vs. other parties-1.png" width="672" />





2) Univariate Distribution of Societal Misrecognition Dimensions 


```r
# summary statistics table of the four misrecognition dimensions
misrec_table <- analysis_weights %>%
  pivot_longer(
    starts_with("misrec_"),
    names_to = "Dimension",
    values_to = "Value"
    ) %>%
  filter(!is.na(Value), !is.na(w_ipfges), w_ipfges > 0) %>%
  group_by(Dimension) %>%
  summarise(
    N = n(),
    Mean = weighted.mean(Value, w_ipfges),
    SD = sqrt(weighted.mean((Value - Mean)^2, w_ipfges)),
    Min = min(Value),
    Max = max(Value),
    .groups = "drop"
   ) %>%
  mutate(
    Dimension = recode(Dimension,
      misrec_economic = "Economic",
      misrec_work = "Work",
      misrec_services = "Basic Services",
      misrec_opinion = "Opinion"
     )
    ) %>%
  arrange(match(Dimension,
                c("Economic", "Work", "Basic Services", "Opinion")))
# output table
knitr::kable(
  misrec_table,
  digits = 2,
  caption = "Descriptive Statistics of Perceived Societal Misrecognition"
 )
```



Table: Descriptive Statistics of Perceived Societal Misrecognition

|Dimension      |    N| Mean|   SD| Min| Max|
|:--------------|----:|----:|----:|---:|---:|
|Economic       | 6887| 0.49| 0.27|   0|   1|
|Work           | 6845| 0.51| 0.29|   0|   1|
|Basic Services | 6839| 0.34| 0.28|   0|   1|
|Opinion        | 6873| 0.28| 0.31|   0|   1|




```r
# plot of weighted means
misrec_table$Dimension <- factor(
  misrec_table$Dimension,
  levels = c("Economic", "Work", "Basic Services", "Opinion")
 )
misrec_table <- misrec_table %>% arrange(Dimension)

ggplot(misrec_table, aes(x = Dimension, y = Mean)) +
  geom_col(fill = "grey80", width = 0.4) +
  geom_text(aes(label = sprintf("%.2f", Mean)),
            vjust = -0.5, size = 3.5) +
  scale_y_continuous(limits = c(0, 1)) +
  labs(
    title = "Perceived Societal Misrecognition by Dimension",
    x = NULL,
    y = "Weighted mean"
   ) +
  theme_minimal() +
  theme(
    plot.title = element_text(hjust = 0.5, size = 11)
  )
```

<img src="master_thesis_files/figure-html/plot weighted means of misrecognition dimensions-1.png" width="672" />



```r
table(analysis_weights$misrec_economic)
```

```
## 
##    0 0.25  0.5 0.75    1 
##  669 1820 2311 1577  510
```

```r
table(analysis_weights$misrec_work)
```

```
## 
##    0 0.25  0.5 0.75    1 
##  772 1848 1798 1744  683
```

```r
table(analysis_weights$misrec_services)
```

```
## 
##    0 0.25  0.5 0.75    1 
## 1978 2304 1469  797  291
```

```r
table(analysis_weights$misrec_opinion)
```

```
## 
##    0 0.25  0.5 0.75    1 
## 3105 1634 1061  689  384
```

```r
# histogram of different dimensions of misrecognition 
misrec_long <- analysis_weights %>%
  dplyr::select(
    misrec_economic, misrec_work,
    misrec_services, misrec_opinion,
    w_ipfges
  ) %>%
  tidyr::pivot_longer(
    cols = starts_with("misrec_"),
    names_to = "dimension",
    values_to = "misrecognition"
  ) %>%
  mutate(
    dimension = factor(
      dimension,
      levels = c("misrec_economic", "misrec_work",
                 "misrec_services", "misrec_opinion"),
      labels = c("Economic", "Work", "Basic Services", "Opinion")
    )
  )

ggplot(
  misrec_long %>% filter(!is.na(misrecognition)),
  aes(x = factor(misrecognition), weight = w_ipfges)
) +
  geom_bar(fill = "#245A81", width = 0.95) +
  facet_wrap(~ dimension, ncol = 2) +
  labs(
    x = "",
    y = "Frequency",
    title = "Distribution of Perceived Societal Misrecognition"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(hjust = 0.5, size = 11),
    strip.text = element_text(face = "bold")
  )
```

<img src="master_thesis_files/figure-html/Distribution of Misrecognition across Dimensions-1.png" width="672" />





```r
# Calculate Pearson's R to check correlation between the dimensions: 
#-------------------------------------------------------
# select variables and weights + remove potential missing values
cor_data <- analysis_weights %>%
  dplyr::select(
    misrec_economic,
    misrec_work,
    misrec_services,
    misrec_opinion,
    w_ipfges
  ) %>%
  tidyr::drop_na()

# calculate weighted covariances
weighted_cor <- cov.wt(
  x = cor_data[, 1:4],
  wt = cor_data$w_ipfges, # use weights
  cor = TRUE # correlation matrix
)$cor
```






II. Bivariate Descriptive Statistics


```r
# prepare data for bivariate descriptive analyses
misrec_vote <- analysis_weights %>%
  filter(!is.na(afd_vote)) %>%
  tidyr::pivot_longer(
    cols = c(misrec_economic, misrec_work,
             misrec_services, misrec_opinion),
    names_to = "Dimension",
    values_to = "Value"
  ) %>%
  filter(!is.na(Value)) %>%
  mutate(
    Dimension = factor(
      Dimension,
      levels = c("misrec_economic", "misrec_work",
                 "misrec_services", "misrec_opinion"),
      labels = c("Economic", "Work", "Basic Services", "Opinion")
    ),
    Vote = factor(
      afd_vote,
      levels = c(1, 0),
      labels = c("AfD", "Other parties")  ) )
```



```r
# plot weighted means by second-vote choice
misrec_vote %>%
  group_by(Dimension, Vote) %>%
  summarise(
    Mean = weighted.mean(Value, w_ipfges),
    .groups = "drop"
   ) %>%
  ggplot(aes(x = Dimension, y = Mean, fill = Vote)) +
  geom_col(position = "dodge", width = 0.5) +
  scale_fill_manual(values = c(
    "AfD" = "#245A81",
    "Other parties" = "#A9C8DF"
   )) +
  scale_y_continuous(limits = c(0, 1)) +
  labs(
    title = "Perceived Misrecognition by Vote Choice",
    x = NULL,
    y = "Weighted mean",
    fill = "Vote choice"
   ) +
  theme_minimal() +
  theme(
    plot.title = element_text(hjust = 0.5, size = 11)
   )
```

<img src="master_thesis_files/figure-html/plot weighted means by vote choice-1.png" width="672" />







```r
# calculate weighted percentages within voter groups
misrec_vote_dist <- misrec_vote %>%
  group_by(Dimension, Vote, Value) %>%
  summarise(
    Weight = sum(w_ipfges),
    .groups = "drop_last"
  ) %>%
  mutate(
    Percentage = 100 * Weight / sum(Weight)
  ) %>%
  ungroup()
```




```r
# plot percentage distributions by vote choice
ggplot(
  misrec_vote_dist,
  aes(x = factor(Value), y = Percentage, fill = Vote)
) +
  geom_col(
    position = position_dodge(width = 0.8),
    width = 0.7
  ) +
  facet_wrap(~ Dimension, ncol = 2) +
  scale_fill_manual(values = c( # colors
    "AfD" = "#245A81",
    "Other parties" = "#A9C8DF"
  )) +
  scale_y_continuous( #scale y-axis
    breaks = seq(0, 50, by = 10),
    minor_breaks = seq(0, 55, by = 5),
    expand = expansion(mult = c(0, 0))
  ) +
  coord_cartesian(ylim = c(0, 55)) +
  labs(
    title = "",
    x = "Perceived Misrecognition Dimension",
    y = "Percentages within Voter Group",
    fill = "Vote choice"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(hjust = 0.5, size = 11),
    strip.text = element_text(face = "bold"), 
    #vertical lines 
    panel.grid.major.x = element_line(color = "grey90", linewidth = 0.2), #vertical 
  panel.grid.major.y = element_line(color = "grey80", linewidth = 0.2),#horizontal
  panel.grid.minor = element_line(color = "grey80", linewidth = 0.15)
  )
```

<img src="master_thesis_files/figure-html/percentage distributions by vote choice-1.png" width="672" />





```r
# show distribution percentage tables
misrec_vote_dist %>%
  dplyr::select(Dimension, Vote, Value, Percentage) %>%
  tidyr::pivot_wider(
    names_from = Value,
    values_from = Percentage
   ) %>%
  mutate(
    across(where(is.numeric), ~ round(.x, 2))
   ) %>%
  group_split(Dimension) %>%
  purrr::walk(~ {
    cat("\n---", as.character(.x$Dimension[1]), "---\n")
    print(
      as.data.frame(dplyr::select(.x, -Dimension)),
      row.names = FALSE )})
```

```
## 
## --- Economic ---
##           Vote    0  0.25   0.5  0.75    1
##            AfD 3.28 11.96 34.96 30.90 18.9
##  Other parties 9.77 28.01 32.73 23.29  6.2
## 
## --- Work ---
##           Vote     0  0.25   0.5  0.75     1
##            AfD  4.92 14.72 25.68 31.81 22.87
##  Other parties 11.38 27.96 25.64 25.89  9.13
## 
## --- Basic Services ---
##           Vote     0  0.25   0.5  0.75    1
##            AfD 15.73 27.43 28.49 19.99 8.37
##  Other parties 29.81 34.51 20.65 11.42 3.63
## 
## --- Opinion ---
##           Vote     0  0.25   0.5  0.75     1
##            AfD  9.08 13.15 22.19 29.92 25.64
##  Other parties 50.17 25.71 13.93  7.59  2.60
```



## III. Regression Analysis 

Binary logistic regression model using the logistic cumulative distribution function 

$$P(Y_i = 1 \mid X_i) = \frac{\exp(X_i\beta)}{1+\exp(X_i\beta)}$$


```r
# 4 models 4 dimensions 

# economic
#-------------------------------
m_economic <- glm(
  afd_vote ~ misrec_economic,
  data = analysis,
  family = quasibinomial(link= "logit"),
   weights = w_ipfges)

m_economic2 <- glm( # with controls 
  afd_vote ~ misrec_economic +
    female + education + east + age,
  data = analysis_weights,
  family = quasibinomial(link = "logit"),
  weights= w_ipfges)

# work
#---------------------------------
m_work <- glm(
  afd_vote ~ misrec_work,
  data = analysis,
  family = quasibinomial(link= "logit"),
  weights = w_ipfges)

m_work2 <- glm( # with controls 
  afd_vote ~ misrec_work +
    female + education + east + age,
  data = analysis_weights,
  family = quasibinomial(link = "logit"),
  weights= w_ipfges)

# basic services 
#--------------------------------
m_services <- glm(
  afd_vote ~ misrec_services,
  data = analysis,
  family = quasibinomial(link= "logit"),
  weights = w_ipfges)

m_services2 <- glm( # with controls 
  afd_vote ~ misrec_services +
    female + education + east + age,
  data = analysis_weights,
  family = quasibinomial(link = "logit"),
  weights= w_ipfges)


# opinion
#---------------------------------
m_opinion <- glm(
  afd_vote ~ misrec_opinion,
  data = analysis,
  family = quasibinomial(link= "logit"),
  weights = w_ipfges)

m_opinion2 <- glm( # with controls 
  afd_vote ~ misrec_opinion +
    female + education + east + age,
  data = analysis_weights,
  family = quasibinomial(link = "logit"),
  weights= w_ipfges)


#output of models 
summary(m_economic)
```

```
## 
## Call:
## glm(formula = afd_vote ~ misrec_economic, family = quasibinomial(link = "logit"), 
##     data = analysis, weights = w_ipfges)
## 
## Coefficients:
##                 Estimate Std. Error t value Pr(>|t|)    
## (Intercept)     -3.01383    0.09561  -31.52   <2e-16 ***
## misrec_economic  2.21688    0.14611   15.17   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for quasibinomial family taken to be 0.9579398)
## 
##     Null deviance: 4754.6  on 6067  degrees of freedom
## Residual deviance: 4516.8  on 6066  degrees of freedom
##   (1268 Beobachtungen als fehlend gelöscht)
## AIC: NA
## 
## Number of Fisher Scoring iterations: 5
```

```r
summary(m_economic2)
```

```
## 
## Call:
## glm(formula = afd_vote ~ misrec_economic + female + education + 
##     east + age, family = quasibinomial(link = "logit"), data = analysis_weights, 
##     weights = w_ipfges)
## 
## Coefficients:
##                  Estimate Std. Error t value Pr(>|t|)    
## (Intercept)     -0.836345   0.202638  -4.127 3.72e-05 ***
## misrec_economic  1.705988   0.157944  10.801  < 2e-16 ***
## female          -0.419682   0.079852  -5.256 1.53e-07 ***
## educationMedium -0.197401   0.098165  -2.011   0.0444 *  
## educationHigh   -1.372436   0.119834 -11.453  < 2e-16 ***
## east             0.809270   0.090132   8.979  < 2e-16 ***
## age             -0.026542   0.002524 -10.514  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for quasibinomial family taken to be 0.9627104)
## 
##     Null deviance: 4648.9  on 5974  degrees of freedom
## Residual deviance: 4098.7  on 5968  degrees of freedom
##   (1125 Beobachtungen als fehlend gelöscht)
## AIC: NA
## 
## Number of Fisher Scoring iterations: 5
```

```r
summary(m_work)
```

```
## 
## Call:
## glm(formula = afd_vote ~ misrec_work, family = quasibinomial(link = "logit"), 
##     data = analysis, weights = w_ipfges)
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept) -2.80208    0.09032  -31.02   <2e-16 ***
## misrec_work  1.79565    0.13437   13.36   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for quasibinomial family taken to be 0.9626546)
## 
##     Null deviance: 4719.3  on 6027  degrees of freedom
## Residual deviance: 4535.4  on 6026  degrees of freedom
##   (1308 Beobachtungen als fehlend gelöscht)
## AIC: NA
## 
## Number of Fisher Scoring iterations: 5
```

```r
summary(m_work2)
```

```
## 
## Call:
## glm(formula = afd_vote ~ misrec_work + female + education + east + 
##     age, family = quasibinomial(link = "logit"), data = analysis_weights, 
##     weights = w_ipfges)
## 
## Coefficients:
##                  Estimate Std. Error t value Pr(>|t|)    
## (Intercept)     -0.674612   0.206645  -3.265   0.0011 ** 
## misrec_work      1.327210   0.147476   8.999  < 2e-16 ***
## female          -0.442814   0.080739  -5.484 4.32e-08 ***
## educationMedium -0.182646   0.098867  -1.847   0.0647 .  
## educationHigh   -1.407261   0.121248 -11.606  < 2e-16 ***
## east             0.820558   0.090873   9.030  < 2e-16 ***
## age             -0.025699   0.002575  -9.978  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for quasibinomial family taken to be 0.979165)
## 
##     Null deviance: 4613.8  on 5934  degrees of freedom
## Residual deviance: 4099.1  on 5928  degrees of freedom
##   (1165 Beobachtungen als fehlend gelöscht)
## AIC: NA
## 
## Number of Fisher Scoring iterations: 5
```

```r
summary(m_services)
```

```
## 
## Call:
## glm(formula = afd_vote ~ misrec_services, family = quasibinomial(link = "logit"), 
##     data = analysis, weights = w_ipfges)
## 
## Coefficients:
##                 Estimate Std. Error t value Pr(>|t|)    
## (Intercept)     -2.38528    0.06456  -36.95   <2e-16 ***
## misrec_services  1.57056    0.12525   12.54   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for quasibinomial family taken to be 0.9530103)
## 
##     Null deviance: 4728.7  on 6036  degrees of freedom
## Residual deviance: 4579.4  on 6035  degrees of freedom
##   (1299 Beobachtungen als fehlend gelöscht)
## AIC: NA
## 
## Number of Fisher Scoring iterations: 4
```

```r
summary(m_services2)
```

```
## 
## Call:
## glm(formula = afd_vote ~ misrec_services + female + education + 
##     east + age, family = quasibinomial(link = "logit"), data = analysis_weights, 
##     weights = w_ipfges)
## 
## Coefficients:
##                  Estimate Std. Error t value Pr(>|t|)    
## (Intercept)     -0.087470   0.177521  -0.493   0.6222    
## misrec_services  1.275916   0.136675   9.335  < 2e-16 ***
## female          -0.434156   0.080320  -5.405 6.72e-08 ***
## educationMedium -0.245396   0.098376  -2.494   0.0126 *  
## educationHigh   -1.506832   0.120533 -12.501  < 2e-16 ***
## east             0.830984   0.090461   9.186  < 2e-16 ***
## age             -0.030937   0.002516 -12.295  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for quasibinomial family taken to be 0.9738128)
## 
##     Null deviance: 4624.3  on 5944  degrees of freedom
## Residual deviance: 4101.9  on 5938  degrees of freedom
##   (1155 Beobachtungen als fehlend gelöscht)
## AIC: NA
## 
## Number of Fisher Scoring iterations: 5
```

```r
summary(m_opinion)
```

```
## 
## Call:
## glm(formula = afd_vote ~ misrec_opinion, family = quasibinomial(link = "logit"), 
##     data = analysis, weights = w_ipfges)
## 
## Coefficients:
##                Estimate Std. Error t value Pr(>|t|)    
## (Intercept)    -3.43683    0.08004  -42.94   <2e-16 ***
## misrec_opinion  4.01534    0.13108   30.63   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for quasibinomial family taken to be 0.9374078)
## 
##     Null deviance: 4752.6  on 6057  degrees of freedom
## Residual deviance: 3636.6  on 6056  degrees of freedom
##   (1278 Beobachtungen als fehlend gelöscht)
## AIC: NA
## 
## Number of Fisher Scoring iterations: 5
```

```r
summary(m_opinion2)
```

```
## 
## Call:
## glm(formula = afd_vote ~ misrec_opinion + female + education + 
##     east + age, family = quasibinomial(link = "logit"), data = analysis_weights, 
##     weights = w_ipfges)
## 
## Coefficients:
##                  Estimate Std. Error t value Pr(>|t|)    
## (Intercept)     -1.501309   0.197744  -7.592 3.63e-14 ***
## misrec_opinion   3.853837   0.138559  27.814  < 2e-16 ***
## female          -0.373422   0.087353  -4.275 1.94e-05 ***
## educationMedium -0.152353   0.108702  -1.402    0.161    
## educationHigh   -1.164772   0.126587  -9.201  < 2e-16 ***
## east             0.855588   0.100161   8.542  < 2e-16 ***
## age             -0.028472   0.002797 -10.178  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for quasibinomial family taken to be 0.9340203)
## 
##     Null deviance: 4648.2  on 5965  degrees of freedom
## Residual deviance: 3322.5  on 5959  degrees of freedom
##   (1134 Beobachtungen als fehlend gelöscht)
## AIC: NA
## 
## Number of Fisher Scoring iterations: 6
```

```r
# first thoughts: all show positive and statistical significant relations - opinion shows the strongest relationship 
```












```r
# first model with all 4 dimensions, without further controls

# unweighted
model1a <- glm(
  afd_vote ~ misrec_economic + misrec_work +
    misrec_services + misrec_opinion,
  data = analysis_weights,
  family = binomial(link = "logit"))
 
summary(model1a)
```

```
## 
## Call:
## glm(formula = afd_vote ~ misrec_economic + misrec_work + misrec_services + 
##     misrec_opinion, family = binomial(link = "logit"), data = analysis_weights)
## 
## Coefficients:
##                 Estimate Std. Error z value Pr(>|z|)    
## (Intercept)      -3.9118     0.1232 -31.763  < 2e-16 ***
## misrec_economic   0.9783     0.2222   4.402 1.07e-05 ***
## misrec_work       0.1394     0.2059   0.677   0.4985    
## misrec_services  -0.3065     0.1725  -1.777   0.0756 .  
## misrec_opinion    3.9428     0.1485  26.552  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 4681.6  on 5971  degrees of freedom
## Residual deviance: 3509.6  on 5967  degrees of freedom
##   (1128 Beobachtungen als fehlend gelöscht)
## AIC: 3519.6
## 
## Number of Fisher Scoring iterations: 6
```

```r
# weighted 
model1b <- glm(
  afd_vote ~ misrec_economic + misrec_work +
    misrec_services + misrec_opinion,
  data = analysis_weights,
  family = quasibinomial(link = "logit"),
  weights = w_ipfges)
 
summary(model1b)
```

```
## 
## Call:
## glm(formula = afd_vote ~ misrec_economic + misrec_work + misrec_services + 
##     misrec_opinion, family = quasibinomial(link = "logit"), data = analysis_weights, 
##     weights = w_ipfges)
## 
## Coefficients:
##                 Estimate Std. Error t value Pr(>|t|)    
## (Intercept)     -3.80392    0.11954 -31.821  < 2e-16 ***
## misrec_economic  0.96085    0.21038   4.567 5.04e-06 ***
## misrec_work      0.06326    0.19402   0.326   0.7444    
## misrec_services -0.31438    0.16129  -1.949   0.0513 .  
## misrec_opinion   3.85406    0.14151  27.235  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for quasibinomial family taken to be 0.922117)
## 
##     Null deviance: 4690.5  on 5971  degrees of freedom
## Residual deviance: 3564.2  on 5967  degrees of freedom
##   (1128 Beobachtungen als fehlend gelöscht)
## AIC: NA
## 
## Number of Fisher Scoring iterations: 5
```




```r
# model with all 4 dimensions and controls 

# unweighted
model2a <- glm(
  afd_vote ~ misrec_economic + misrec_work +
    misrec_services + misrec_opinion +
    female + education + east + age,
  data = analysis_weights,
  family = binomial(link = "logit"))

summary(model2a)
```

```
## 
## Call:
## glm(formula = afd_vote ~ misrec_economic + misrec_work + misrec_services + 
##     misrec_opinion + female + education + east + age, family = binomial(link = "logit"), 
##     data = analysis_weights)
## 
## Coefficients:
##                  Estimate Std. Error z value Pr(>|z|)    
## (Intercept)     -2.520064   0.264338  -9.533  < 2e-16 ***
## misrec_economic  0.708574   0.232917   3.042  0.00235 ** 
## misrec_work     -0.088676   0.218610  -0.406  0.68501    
## misrec_services -0.400741   0.182321  -2.198  0.02795 *  
## misrec_opinion   3.988798   0.157435  25.336  < 2e-16 ***
## female          -0.394163   0.092591  -4.257 2.07e-05 ***
## educationMedium  0.118255   0.142270   0.831  0.40586    
## educationHigh   -0.791672   0.149448  -5.297 1.18e-07 ***
## east             0.882789   0.095207   9.272  < 2e-16 ***
## age             -0.018362   0.002893  -6.347 2.19e-10 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 4610.6  on 5880  degrees of freedom
## Residual deviance: 3241.3  on 5871  degrees of freedom
##   (1219 Beobachtungen als fehlend gelöscht)
## AIC: 3261.3
## 
## Number of Fisher Scoring iterations: 6
```

```r
# weighted
#main model:
model2b <- glm(
  afd_vote ~ misrec_economic + misrec_work +
    misrec_services + misrec_opinion +
    female + education + east + age,
  data = analysis_weights,
  family = quasibinomial(link = "logit"),
  weights= w_ipfges)

summary(model2b)
```

```
## 
## Call:
## glm(formula = afd_vote ~ misrec_economic + misrec_work + misrec_services + 
##     misrec_opinion + female + education + east + age, family = quasibinomial(link = "logit"), 
##     data = analysis_weights, weights = w_ipfges)
## 
## Coefficients:
##                  Estimate Std. Error t value Pr(>|t|)    
## (Intercept)     -1.640370   0.237576  -6.905 5.57e-12 ***
## misrec_economic  0.755501   0.221332   3.413 0.000646 ***
## misrec_work     -0.308151   0.208362  -1.479 0.139216    
## misrec_services -0.349803   0.171149  -2.044 0.041013 *  
## misrec_opinion   3.841185   0.150193  25.575  < 2e-16 ***
## female          -0.368508   0.087906  -4.192 2.80e-05 ***
## educationMedium -0.133507   0.110019  -1.213 0.224991    
## educationHigh   -1.171980   0.130789  -8.961  < 2e-16 ***
## east             0.828365   0.101316   8.176 3.56e-16 ***
## age             -0.027687   0.002905  -9.532  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for quasibinomial family taken to be 0.9279877)
## 
##     Null deviance: 4586.1  on 5880  degrees of freedom
## Residual deviance: 3270.3  on 5871  degrees of freedom
##   (1219 Beobachtungen als fehlend gelöscht)
## AIC: NA
## 
## Number of Fisher Scoring iterations: 6
```




```r
# model with index

# unweighted data
model3a <- glm(
  afd_vote ~ misrecog_index,
  data = analysis_weights,
  family = binomial(link = "logit"))

summary(model3a)
```

```
## 
## Call:
## glm(formula = afd_vote ~ misrecog_index, family = binomial(link = "logit"), 
##     data = analysis_weights)
## 
## Coefficients:
##                Estimate Std. Error z value Pr(>|z|)    
## (Intercept)    -3.18467    0.07633  -41.73   <2e-16 ***
## misrecog_index  4.37160    0.18397   23.76   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 4681.6  on 5971  degrees of freedom
## Residual deviance: 4052.8  on 5970  degrees of freedom
##   (1128 Beobachtungen als fehlend gelöscht)
## AIC: 4056.8
## 
## Number of Fisher Scoring iterations: 5
```

```r
# weighted data
model3b <- glm(
  afd_vote ~ misrecog_index,
  data = analysis_weights,
  family = quasibinomial(link = "logit"),
  weights= w_ipfges)

summary(model3b)
```

```
## 
## Call:
## glm(formula = afd_vote ~ misrecog_index, family = quasibinomial(link = "logit"), 
##     data = analysis_weights, weights = w_ipfges)
## 
## Coefficients:
##                Estimate Std. Error t value Pr(>|t|)    
## (Intercept)    -3.10998    0.07349  -42.32   <2e-16 ***
## misrecog_index  4.19563    0.17195   24.40   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for quasibinomial family taken to be 0.9069096)
## 
##     Null deviance: 4690.5  on 5971  degrees of freedom
## Residual deviance: 4091.1  on 5970  degrees of freedom
##   (1128 Beobachtungen als fehlend gelöscht)
## AIC: NA
## 
## Number of Fisher Scoring iterations: 5
```






```r
# Robustness Checks

#alternative operationalization of age:

model_cat <- glm(
  afd_vote ~ misrec_economic + misrec_work +
    misrec_services + misrec_opinion +
    female + education + east + as.factor(age_group),
  data = analysis_weights,
  family = quasibinomial(link = "logit"),
  weights= w_ipfges)


summary(model_cat)
```

```
## 
## Call:
## glm(formula = afd_vote ~ misrec_economic + misrec_work + misrec_services + 
##     misrec_opinion + female + education + east + as.factor(age_group), 
##     family = quasibinomial(link = "logit"), data = analysis_weights, 
##     weights = w_ipfges)
## 
## Coefficients:
##                           Estimate Std. Error t value Pr(>|t|)    
## (Intercept)               -2.69200    0.21124 -12.744  < 2e-16 ***
## misrec_economic            0.76938    0.22266   3.455 0.000553 ***
## misrec_work               -0.23896    0.20882  -1.144 0.252513    
## misrec_services           -0.38258    0.17176  -2.227 0.025956 *  
## misrec_opinion             3.83862    0.15126  25.377  < 2e-16 ***
## female                    -0.38448    0.08816  -4.361 1.32e-05 ***
## educationMedium           -0.04281    0.10851  -0.394 0.693234    
## educationHigh             -1.04931    0.12858  -8.160 4.05e-16 ***
## east                       0.80062    0.10150   7.888 3.64e-15 ***
## as.factor(age_group)30-44 -0.09808    0.15861  -0.618 0.536364    
## as.factor(age_group)45-59 -0.33029    0.15999  -2.064 0.039024 *  
## as.factor(age_group)60+   -1.03073    0.16579  -6.217 5.41e-10 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for quasibinomial family taken to be 0.9395777)
## 
##     Null deviance: 4586.1  on 5880  degrees of freedom
## Residual deviance: 3286.9  on 5869  degrees of freedom
##   (1219 Beobachtungen als fehlend gelöscht)
## AIC: NA
## 
## Number of Fisher Scoring iterations: 6
```

```r
# model with even more controls 
model5 <- glm(
  afd_vote ~ misrec_economic + misrec_work +
    misrec_services + misrec_opinion +
    female + education + east + age +
    right_ideology + econ_situ + rural ,
  data = analysis_weights,
  family = quasibinomial(link = "logit"),
  weights= w_ipfges)


summary(model5)
```

```
## 
## Call:
## glm(formula = afd_vote ~ misrec_economic + misrec_work + misrec_services + 
##     misrec_opinion + female + education + east + age + right_ideology + 
##     econ_situ + rural, family = quasibinomial(link = "logit"), 
##     data = analysis_weights, weights = w_ipfges)
## 
## Coefficients:
##                  Estimate Std. Error t value Pr(>|t|)    
## (Intercept)     -3.135349   0.277111 -11.314  < 2e-16 ***
## misrec_economic  0.504249   0.239114   2.109  0.03500 *  
## misrec_work     -0.304850   0.220808  -1.381  0.16745    
## misrec_services -0.500719   0.179411  -2.791  0.00527 ** 
## misrec_opinion   3.590273   0.155687  23.061  < 2e-16 ***
## female          -0.197655   0.093026  -2.125  0.03365 *  
## educationMedium -0.141492   0.115256  -1.228  0.21964    
## educationHigh   -1.033473   0.135821  -7.609 3.22e-14 ***
## east             0.976260   0.107401   9.090  < 2e-16 ***
## age             -0.020174   0.003046  -6.623 3.85e-11 ***
## right_ideology   1.200201   0.095796  12.529  < 2e-16 ***
## econ_situ        1.874204   0.229889   8.153 4.35e-16 ***
## rural            0.259020   0.094075   2.753  0.00592 ** 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for quasibinomial family taken to be 0.8977008)
## 
##     Null deviance: 4361.1  on 5663  degrees of freedom
## Residual deviance: 2926.5  on 5651  degrees of freedom
##   (1436 Beobachtungen als fehlend gelöscht)
## AIC: NA
## 
## Number of Fisher Scoring iterations: 6
```










```r
# model with index and controls
model4b <- glm(
  afd_vote ~ misrecog_index +
    female + education + east + age,
  data = analysis_weights,
  family = quasibinomial(link = "logit"),
  weights= w_ipfges)

summary(model4b)
```

```
## 
## Call:
## glm(formula = afd_vote ~ misrecog_index + female + education + 
##     east + age, family = quasibinomial(link = "logit"), data = analysis_weights, 
##     weights = w_ipfges)
## 
## Coefficients:
##                  Estimate Std. Error t value Pr(>|t|)    
## (Intercept)     -1.272161   0.189956  -6.697 2.32e-11 ***
## misrecog_index   3.681191   0.182372  20.185  < 2e-16 ***
## female          -0.471248   0.081329  -5.794 7.21e-09 ***
## educationMedium -0.091740   0.100827  -0.910    0.363    
## educationHigh   -1.125906   0.120467  -9.346  < 2e-16 ***
## east             0.735954   0.092212   7.981 1.73e-15 ***
## age             -0.023831   0.002571  -9.269  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for quasibinomial family taken to be 0.9048093)
## 
##     Null deviance: 4586.1  on 5880  degrees of freedom
## Residual deviance: 3760.8  on 5874  degrees of freedom
##   (1219 Beobachtungen als fehlend gelöscht)
## AIC: NA
## 
## Number of Fisher Scoring iterations: 5
```











## IV. Quantities of Interest

Simulation of Predicted Probabilities 


```r
library(MASS)
library(ggplot2)

# 1. Get coefficients and variance-covariance matrix
beta_hat <- coef(model2b)
V_hat <- vcov(model2b)

# 2. Simulate parameters
set.seed(123)
nsim <- 10000

S <- MASS::mvrnorm(
  n = nsim,
  mu = beta_hat,
  Sigma = V_hat
)

# 3. Get model data and estimation weights
model_data <- model.frame(model2b)
model_weights <- weights(model2b, type = "prior")

# 4. Define values of economic misrecognition
seq_X <- seq(0, 1, by = 0.25)

# 5. Calculate simulated average predicted probabilities
results <- lapply(seq_X, function(x) {

  scenario <- model_data
  scenario$misrec_economic <- x

  X <- model.matrix(
    delete.response(terms(model2b)),
    data = scenario,
    contrasts.arg = model2b$contrasts
  )

  # Simulated probabilities for each respondent
  p_sim <- plogis(X %*% t(S))

  # Weighted average across respondents
  p_avg <- colSums(
    p_sim * model_weights
  ) / sum(model_weights)

  data.frame(
    misrec_economic = x,
    p_mean = mean(p_avg),
    ci_lo = unname(quantile(p_avg, 0.025)),
    ci_hi = unname(quantile(p_avg, 0.975))
  )
})

plot_df <- do.call(rbind, results)

plot_df
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["misrec_economic"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["p_mean"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["ci_lo"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["ci_hi"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"0.00","2":"0.1087810","3":"0.08948265","4":"0.1295538"},{"1":"0.25","2":"0.1231596","3":"0.10976125","4":"0.1370326"},{"1":"0.50","2":"0.1390270","3":"0.13099406","4":"0.1472125"},{"1":"0.75","2":"0.1564390","3":"0.14591192","4":"0.1676684"},{"1":"1.00","2":"0.1754388","3":"0.15490510","4":"0.1980131"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>




```r
# predicted probabilities 
# check for one dimension 
ggplot(plot_df, aes(x = misrec_economic, y = p_mean)) +

  # Shaded 95% confidence interval
  geom_ribbon(
    aes(ymin = ci_lo, ymax = ci_hi),
    fill = "#A9C8DF",
    alpha = 0.7
  ) +

  # Predicted probability
  geom_line(
    color = "#245A81",
    linewidth = 1.1
  ) +

  geom_point(
    color = "#245A81",
    size = 2
  ) +

  scale_x_continuous(
    breaks = seq(0, 1, by = 0.25)
  ) +

  scale_y_continuous(
    labels = function(x) paste0(round(x * 100), "%")
  ) +

  labs(
    title = "Predicted Probability of AfD Voting",
    subtitle = "Economic Misrecognition",
    x = "Perceived economic misrecognition",
    y = "Predicted probability of AfD voting",
    caption = "Shaded area indicates the 95% confidence interval."
  ) +

  theme_minimal() +

  theme(
    plot.title = element_text(hjust = 0.5, size = 11),
    plot.subtitle = element_text(hjust = 0.5)
  )
```

<img src="master_thesis_files/figure-html/plot pp-1.png" width="672" />




```r
# predicted probabilities of AfD voting 


library(MASS)
library(dplyr)
library(ggplot2)

# Simulate parameters
set.seed(123)

nsim <- 10000

S <- MASS::mvrnorm(
  n = nsim,
  mu = coef(model2b),
  Sigma = vcov(model2b)
)

# Data and weights used in model2b
model_data <- model.frame(model2b)
model_weights <- weights(model2b, type = "prior")

# Four dimensions
dimensions <- c(
  "misrec_economic",
  "misrec_work",
  "misrec_services",
  "misrec_opinion"
)

# Values of misrecognition
seq_X <- seq(0, 1, by = 0.25)

# Simulate predicted probabilities
results_all <- lapply(dimensions, function(v) {

  results_dimension <- lapply(seq_X, function(x) {

    scenario <- model_data
    scenario[[v]] <- x

    X <- model.matrix(
      delete.response(terms(model2b)),
      data = scenario,
      contrasts.arg = model2b$contrasts
    )

    p_sim <- plogis(X %*% t(S))

    p_avg <- colSums(
      p_sim * model_weights
    ) / sum(model_weights)

    data.frame(
      Dimension = v,
      Value = x,
      p_mean = mean(p_avg),
      ci_lo = unname(quantile(p_avg, 0.025)),
      ci_hi = unname(quantile(p_avg, 0.975))
    )
  })

  bind_rows(results_dimension)
})

plot_df_all <- bind_rows(results_all)

# Readable dimension labels
plot_df_all <- plot_df_all %>%
  mutate(
    Dimension = factor(
      Dimension,
      levels = dimensions,
      labels = c(
        "Economic",
        "Work",
        "Basic Services",
        "Opinion"
      )
    )
  )
```









```r
# plot predicted probabilities for afd vote  for all 4 dimensions

library(ggh4x)



# predicted probability plot of afd vote with shaded CI and different y axes
#-----------------------------------------------------------------------
plot_shaded <- ggplot(plot_df_all, aes(x = Value)) +

  # Shaded 95% confidence interval
  geom_ribbon(
    aes(ymin = ci_lo, ymax = ci_hi),
    fill = "#7FA9C7",
    alpha = 0.7
  ) +
  # Predicted probability
  geom_line(
    aes(y = p_mean),
    color = "#245A81",
    linewidth = 1.1
  ) +
  facet_wrap(
    ~ Dimension,
    ncol = 2
  ) +
  scale_x_continuous(
    breaks = seq(0, 1, by = 0.25)
  ) +
  scale_y_continuous(
  limits = c(0, 0.7),
  breaks = seq(0, 1, by = 0.2)
) +
  labs(
    title = "",
    subtitle = "",
    x = "Perceived misrecognition",
    y = "Predicted probability of AfD voting",
    caption = "Note: Shaded areas indicate simulated 95% confidence intervals."
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(hjust = 0.5, size = 11),
    plot.subtitle = element_text(hjust = 0.5),
    strip.text = element_text(face = "bold")
  )

plot_shaded #at the moment = favorite one 
```

<img src="master_thesis_files/figure-html/Plot of predicted probabilities 2-1.png" width="672" />

```r
# alternative plot of predicted probabilities with shaded CI 
#--------------------------------------------------------------
plot_shaded_alt <- ggplot(
  plot_df_all,
  aes(x = Value)
) +
  # Shaded 95% confidence interval
  geom_ribbon(
    aes(
      ymin = ci_lo,
      ymax = ci_hi,
      fill = "95% CI"
    ),
    alpha = 0.7
  ) +
  # Predicted probability
  geom_line(
    aes(
      y = p_mean,
      color = "Predicted probability"
    ),
    linewidth = 1.1
  ) +
  ggh4x::facet_wrap2(
    ~ Dimension,
    ncol = 2,
    scales = "free_y",
    axes = "all"
  ) +
  ggh4x::facetted_pos_scales(
    y = list(
      Dimension %in% c(
        "Economic", "Work", "Basic Services"
      ) ~
        scale_y_continuous(
          limits = c(0, 0.25),
          labels = function(x) paste0(round(x * 100), "%")
        ),
      Dimension == "Opinion" ~
        scale_y_continuous(
          limits = c(0, 0.65),
          labels = function(x) paste0(round(x * 100), "%")
        )
    )
  ) +
  scale_fill_manual(
    name = NULL,
    values = c("95% CI" = "#7FA9C7")
  ) +
  scale_color_manual(
    name = NULL,
    values = c("Predicted probability" = "#245A81")
  ) +
  scale_x_continuous(
    breaks = seq(0, 1, by = 0.25)
  ) +
  labs(
    title = "",
    subtitle = "",
    x = "Perceived misrecognition",
    y = "Predicted probability of AfD voting",
    caption = "Note: Shaded areas indicate simulated 95% confidence intervals. Opinion uses a different y-axis scale."
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(hjust = 0.5, size = 11),
    plot.subtitle = element_text(hjust = 0.5),
    strip.text = element_text(face = "bold"),
    legend.position = "bottom",
    legend.box = "horizontal"
  )

plot_shaded_alt
```

<img src="master_thesis_files/figure-html/Plot of predicted probabilities 2-2.png" width="672" />

```r
# save plots 
pdf(
  "predicted_probabilities_comparison.pdf",
  width = 9,
  height = 6.5
)

print(plot_shaded)
print(plot_shaded_alt)

dev.off()
```

```
## png 
##   2
```





# Average First Differences 

```r
library(MASS)
library(dplyr)
library(ggplot2)

set.seed(123)

nsim <- 10000

# Simulate coefficients
S <- MASS::mvrnorm(
  n = nsim,
  mu = coef(model2b),
  Sigma = vcov(model2b)
)

# Model data and weights
model_data <- model.frame(model2b)
model_weights <- weights(model2b, type = "prior")

# Four dimensions
dimensions <- c(
  "misrec_economic",
  "misrec_work",
  "misrec_services",
  "misrec_opinion"
)

# Calculate weighted average first differences
afd_results <- lapply(dimensions, function(v) {

  # Scenario 0: minimum misrecognition
  scenario_0 <- model_data
  scenario_0[[v]] <- 0

  # Scenario 1: maximum misrecognition
  scenario_1 <- model_data
  scenario_1[[v]] <- 1

  X0 <- model.matrix(
    delete.response(terms(model2b)),
    data = scenario_0,
    contrasts.arg = model2b$contrasts
  )

  X1 <- model.matrix(
    delete.response(terms(model2b)),
    data = scenario_1,
    contrasts.arg = model2b$contrasts
  )

  # Weighted mean predicted probability for each simulation
  p0 <- colSums(
    plogis(X0 %*% t(S)) * model_weights
  ) / sum(model_weights)

  p1 <- colSums(
    plogis(X1 %*% t(S)) * model_weights
  ) / sum(model_weights)

  # First difference within each simulation
  fd_sim <- p1 - p0

  data.frame(
    Dimension = v,
    AFD = mean(fd_sim),
    ci_lo = unname(quantile(fd_sim, 0.025)),
    ci_hi = unname(quantile(fd_sim, 0.975))
  )
})

afd_df <- dplyr::bind_rows(afd_results) %>%
  mutate(
    Dimension = factor(
      Dimension,
      levels = dimensions,
      labels = c(
        "Economic",
        "Work",
        "Basic Services",
        "Opinion"
      )
    )
  )

afd_df
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["Dimension"],"name":[1],"type":["fct"],"align":["left"]},{"label":["AFD"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["ci_lo"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["ci_hi"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"Economic","2":"0.06665786","3":"0.02793304","4":"0.105916870"},{"1":"Work","2":"-0.02707011","3":"-0.06338209","4":"0.008829147"},{"1":"Basic Services","2":"-0.03002348","3":"-0.05756810","4":"-0.001145777"},{"1":"Opinion","2":"0.52515730","3":"0.48155125","4":"0.568459527"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>



```r
plot_afd <- ggplot(
  afd_df,
  aes(x = AFD * 100, y = Dimension)
) +

  geom_vline(
    xintercept = 0,
    linetype = "dashed",
    color = "grey50"
  ) +

  geom_errorbarh(
    aes(
      xmin = ci_lo * 100,
      xmax = ci_hi * 100
    ),
    height = 0.15,
    color = "#245A81",
    linewidth = 0.8
  ) +

  geom_point(
    color = "#245A81",
    size = 2.8
  ) +

  labs(
    title = "Average First Differences in AfD Voting Probability",
    subtitle = "Change from Minimum to Maximum Perceived Misrecognition",
    x = "Change in predicted probability (percentage points)",
    y = NULL,
    caption = "Points represent weighted average first differences; horizontal lines indicate simulated 95% confidence intervals."
  ) +

  theme_minimal() +

  theme(
    plot.title = element_text(hjust = 0.5, size = 11),
    plot.subtitle = element_text(hjust = 0.5)
  )
```

```
## Warning: `geom_errorbarh()` was deprecated in ggplot2 4.0.0.
## ℹ Please use the `orientation` argument of `geom_errorbar()` instead.
## This warning is displayed once every 8 hours.
## Call `lifecycle::last_lifecycle_warnings()` to see where this warning was
## generated.
```

```r
plot_afd
```

```
## `height` was translated to `width`.
```

<img src="master_thesis_files/figure-html/Plot first differences-1.png" width="672" />

```r
############

library(ggplot2)
library(dplyr)

afd_plot_df <- afd_df %>%
  mutate(
    Dimension = reorder(Dimension, AFD),
    label = sprintf("%+.1f pp", AFD * 100)
  )

plot_afd_beautiful <- ggplot(
  afd_plot_df,
  aes(x = AFD * 100, y = Dimension)
) +

  # Zero reference line
  geom_vline(
    xintercept = 0,
    color = "grey45",
    linetype = "dashed",
    linewidth = 0.6
  ) +

  # 95% confidence intervals
  geom_errorbar(
    aes(
      xmin = ci_lo * 100,
      xmax = ci_hi * 100
    ),
    orientation = "y",
    width = 0.15,
    color = "#245A81",
    linewidth = 0.9
  ) +

  # Point estimates
  geom_point(
    color = "#245A81",
    size = 3.5
  ) +

  # Value labels – to the right of the confidence intervals
geom_text(
  aes(
    x = ci_hi * 100 + 1.5,
    label = label
  ),
  hjust = 0,
  size = 3.5,
  color = "#245A81",
  fontface = "bold"
) +

  scale_x_continuous(
    breaks = seq(-10, 60, by = 10),
    limits = c(-11, 68)
  ) +

  labs(
    title = "",
    subtitle = "",
    x = "Change in predicted probability (percentage points)",
    y = NULL,
    caption = paste(
      "",
      ""
    )
  ) +

  theme_minimal(base_size = 12) +

  theme(
    plot.title = element_text(
      face = "bold",
      size = 13
    ),
    plot.subtitle = element_text(
      size = 10,
      color = "grey35"
    ),
    axis.text.y = element_text(
      size = 11,
      face = "bold"
    ),
    axis.text.x = element_text(size = 10),
    panel.grid.major.y = element_blank(),
    panel.grid.minor = element_blank(),
    plot.caption = element_text(
      size = 8,
      color = "grey40",
      hjust = 0
    ),
    plot.margin = margin(15, 25, 15, 15)
  )

plot_afd_beautiful
```

<img src="master_thesis_files/figure-html/Plot first differences-2.png" width="672" />





```r
#Predicted Probabilities for afd vote:  misrecognition index

formula(model4b)
```

```
## afd_vote ~ misrecog_index + female + education + east + age
```

```r
names(model.frame(model4b))
```

```
## [1] "afd_vote"       "misrecog_index" "female"         "education"     
## [5] "east"           "age"            "(weights)"
```

```r
set.seed(123)

S_index <- MASS::mvrnorm(
  n = 10000,
  mu = coef(model4b),
  Sigma = vcov(model4b)
)

index_data <- model.frame(model4b)
index_weights <- weights(model4b, type = "prior")

# Replace with the actual variable name from model4b
index_var <- "misrecog_index"

index_values <- seq(0, 1, by = 0.05)

index_results <- lapply(index_values, function(x) {

  scenario <- index_data
  scenario[[index_var]] <- x

  X <- model.matrix(
    delete.response(terms(model4b)),
    data = scenario,
    contrasts.arg = model4b$contrasts
  )

  p_sim <- plogis(X %*% t(S_index))

  p_avg <- colSums(
    p_sim * index_weights
  ) / sum(index_weights)

  data.frame(
    Index = x,
    p_mean = mean(p_avg),
    ci_lo = unname(quantile(p_avg, 0.025)),
    ci_hi = unname(quantile(p_avg, 0.975))
  )
})

index_plot_df <- dplyr::bind_rows(index_results)
```



```r
# plot predicted probabilities afd_vote with misrecognition index


plot_index <- ggplot(index_plot_df, aes(x = Index)) +

  geom_ribbon(
    aes(ymin = ci_lo, ymax = ci_hi, fill = "95% CI"),
    alpha = 0.6
  ) +

  geom_line(
    aes(y = p_mean, color = "Predicted probability"),
    linewidth = 1.1
  ) +

  scale_fill_manual(
    name = NULL,
    values = c("95% CI" = "#7FA9C7")
  ) +

  scale_color_manual(
    name = NULL,
    values = c("Predicted probability" = "#245A81")
  ) +

  scale_x_continuous(
    breaks = seq(0, 1, by = 0.2)
  ) +

  scale_y_continuous(
    labels = function(x) sprintf("%.1f", x)
  ) +

  coord_cartesian(ylim = c(0, 0.8)) +

  labs(
    title = "Predicted Probability of AfD Voting",
    subtitle = "Squared Index of Perceived Misrecognition",
    x = "Squared misrecognition index",
    y = "Predicted probability of AfD voting",
    caption = "Shaded area indicates the simulated 95% confidence interval."
  ) +

  theme_minimal(base_size = 11) +

  theme(
    plot.title = element_text(hjust = 0.5, face = "bold"),
    plot.subtitle = element_text(hjust = 0.5),
    legend.position = "bottom",
    panel.grid.minor = element_blank()
  )

plot_index
```

<img src="master_thesis_files/figure-html/plot pp with index-1.png" width="672" />



## V. Assessing Model Fit 


```r
# ROC Curve 


library(pROC)
library(ggplot2)

# Observed AfD vote
y <- model.response(model.frame(model2b))

# Predicted AfD voting probabilities
p <- predict(model2b, type = "response")

# ROC curve
roc_model2b <- pROC::roc(
  response = y,
  predictor = p,
  levels = c(0, 1),
  direction = "<",
  quiet = TRUE
)

# Area under the ROC curve
pROC::auc(roc_model2b)
```

```
## Area under the curve: 0.8632
```

```r
roc_df <- data.frame(
  FPR = 1 - roc_model2b$specificities,
  TPR = roc_model2b$sensitivities
)

plot_roc <- ggplot(
  roc_df,
  aes(x = FPR, y = TPR)
) +

  geom_abline(
    intercept = 0,
    slope = 1,
    linetype = "dashed",
    color = "grey60"
  ) +

  geom_path(
    color = "#245A81",
    linewidth = 1.1
  ) +

  coord_equal() +

  scale_x_continuous(
    limits = c(0, 1),
    breaks = seq(0, 1, 0.2)
  ) +

  scale_y_continuous(
    limits = c(0, 1),
    breaks = seq(0, 1, 0.2)
  ) +

  labs(
    title = "ROC Curve for AfD Voting",
    subtitle = paste0(
      "Main Model (AUC = ",
      round(as.numeric(pROC::auc(roc_model2b)), 3),
      ")"
    ),
    x = "False Positive Rate (1 - Specificity)",
    y = "True Positive Rate (Sensitivity)"
  ) +

  theme_minimal(base_size = 11) +

  theme(
    plot.title = element_text(hjust = 0.5, face = "bold"),
    plot.subtitle = element_text(hjust = 0.5),
    panel.grid.minor = element_blank()
  )

plot_roc
```

<img src="master_thesis_files/figure-html/roc curve to test model fit-1.png" width="672" />



```r
# ROC Curve controls 

library(ggplot2)
library(pROC)

# Same observations as model2b
data_compare <- model.frame(model2b)
data_compare$w_ipfges <- weights(model2b, type = "prior")

# Control-only model
model_controls <- glm(
  afd_vote ~ female + education + east + age,
  data = data_compare,
  weights = w_ipfges,
  family = quasibinomial(link = "logit")
)

# Observed outcome
y_compare <- model.response(model.frame(model2b))

# Predicted probabilities
p_controls <- predict(model_controls, type = "response")
p_full <- predict(model2b, type = "response")

# ROC curves
roc_controls <- pROC::roc(
  y_compare, p_controls,
  levels = c(0, 1),
  direction = "<",
  quiet = TRUE
)

roc_full <- pROC::roc(
  y_compare, p_full,
  levels = c(0, 1),
  direction = "<",
  quiet = TRUE
)

# Compare AUC values
data.frame(
  Model = c("Controls only", "Full model"),
  AUC = c(
    as.numeric(pROC::auc(roc_controls)),
    as.numeric(pROC::auc(roc_full))
  )
)
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["Model"],"name":[1],"type":["chr"],"align":["left"]},{"label":["AUC"],"name":[2],"type":["dbl"],"align":["right"]}],"data":[{"1":"Controls only","2":"0.7121684"},{"1":"Full model","2":"0.8632140"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

```r
roc_plot_df <- rbind(
  data.frame(
    FPR = 1 - roc_controls$specificities,
    TPR = roc_controls$sensitivities,
    Model = "Controls only"
  ),
  data.frame(
    FPR = 1 - roc_full$specificities,
    TPR = roc_full$sensitivities,
    Model = "Full model"
  )
)

plot_roc_compare <- ggplot(
  roc_plot_df,
  aes(x = FPR, y = TPR, color = Model)
) +

  geom_abline(
    intercept = 0,
    slope = 1,
    linetype = "dashed",
    color = "grey65"
  ) +

  geom_path(linewidth = 1.1) +

  scale_color_manual(
    values = c(
      "Controls only" = "#9BA5AE",
      "Full model" = "#245A81"
    ),
    labels = c(
      "Controls only" = paste0(
        "Controls only (AUC = ",
        round(as.numeric(pROC::auc(roc_controls)), 3),
        ")"
      ),
      "Full model" = paste0(
        "Full model (AUC = ",
        round(as.numeric(pROC::auc(roc_full)), 3),
        ")"
      )
    )
  ) +

  coord_equal() +

  scale_x_continuous(
    limits = c(0, 1),
    breaks = seq(0, 1, 0.2)
  ) +

  scale_y_continuous(
    limits = c(0, 1),
    breaks = seq(0, 1, 0.2)
  ) +

  labs(
    title = "ROC Curves for AfD Voting",
    subtitle = "Control Model vs. Full Model",
    x = "False Positive Rate (1 - Specificity)",
    y = "True Positive Rate (Sensitivity)",
    color = NULL
  ) +

  theme_minimal(base_size = 11) +

  theme(
    plot.title = element_text(hjust = 0.5, face = "bold"),
    plot.subtitle = element_text(hjust = 0.5),
    legend.position = "bottom",
    panel.grid.minor = element_blank()
  )

plot_roc_compare
```

<img src="master_thesis_files/figure-html/roc controls-1.png" width="672" />





```r
# Separation Plot 

library(separationplot)

separationplot(
  pred = p,
  actual = y,
  line = TRUE,
  heading = "Separation Plot for AfD Voting",
  show.expected = TRUE,
  col0 = "#D9E5ED",
  col1 = "#245A81",
  lwd2 = 2,
  height = 2,
  newplot = FALSE
)
```

<img src="master_thesis_files/figure-html/separation plots-1.png" width="672" />

```r
# check different colors 
library(separationplot)

p_full <- predict(model2b, type = "response")
y_compare <- model.response(model.frame(model2b))

separationplot(
  pred = p_full,
  actual = y_compare,
  line = TRUE,
  heading = "Separation Plot for AfD Voting",
  show.expected = TRUE,
  col0 = "orange",
  col1 = "red",
  lwd2 = 2,
  height = 2.5,
  newplot = FALSE
)
```

<img src="master_thesis_files/figure-html/separation plots-2.png" width="672" />








