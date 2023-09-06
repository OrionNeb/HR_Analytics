---
title: "HR_Analytics2"
author: "Christian Roth"
date: "2023-09-03"
output: 
  html_document:
    keep_md: true
    css: styles.css
    #code_folding: hide
    toc: true
    toc_float: true
    toc_depth: 3
    df_print: paged
bibliography: meine_referenzen.bib
csl: apa.csl
---






# 1. Business Understanding

## 1.1 Zielsetzung

Das übergeordnete Ziel dieses Berichts ist es, die Faktoren zu identifizieren und zu analysieren, die die Jobzufriedenheit von Mitarbeitern beeinflussen. Dabei möchten wir insbesondere verstehen, wie verschiedene Aspekte wie Gehalt, Arbeitsbedingungen, Mitarbeiterbeziehungen und anerkannte Arbeitsleistung die Zufriedenheit am Arbeitsplatz beeinflussen. Die Ergebnisse dieser Analyse sollen als Grundlage für HR-Entscheidungen und -Strategien dienen, um die Mitarbeiterzufriedenheit und -bindung zu verbessern.

## 1.2 Fragen, die beantwortet werden sollen

* Welche Faktoren haben den größten Einfluss auf die Jobzufriedenheit?  
* Wie korrelieren Gehalt, Arbeitsbedingungen und andere Variablen mit der Jobzufriedenheit?  
* Welche Empfehlungen können wir für die Personalabteilung ableiten, um die Mitarbeiterzufriedenheit zu verbessern?  

## 1.3 Aktualisierte These

Die zentrale These dieses Berichts lautet:  

**"Mitarbeiter, die ein höheres Gehalt erhalten, bessere Arbeitsbedingungen vorfinden, positive Mitarbeiterbeziehungen pflegen und deren Arbeitsleistung anerkannt wird bzw. deren Arbeitsanforderungen erfüllbar sind, haben eine höhere Jobzufriedenheit."**  

In diesem Zusammenhang werden spezifische Variablen wie **"MonthlyIncome"**, **"WorkLifeBalance"**, **"RelationshipSatisfaction"** und andere näher betrachtet und analysiert.

## 1.4 Methodik

Dieser Bericht wird nach dem **Cross-Industry Standard Process for Data Mining (CRISP-DM)** entwickelt. Dieses standardisierte Vorgehensmodell ermöglicht eine strukturierte und effiziente Analyse von Datensätzen und ist branchenübergreifend anerkannt. 

Der CRISP-DM-Leitfaden (Cross-Industry Standard Process for Data Mining) wurde ursprünglich im Jahr 1999 veröffentlicht. Dieser Leitfaden stellt ein Rahmenwerk für den Prozess der Datenanalyse und des Data Mining vor und hat zum Ziel, den gesamten Lebenszyklus eines Data-Mining-Projekts zu strukturieren. Der Leitfaden wurde von einem Konsortium entwickelt, das Unternehmen wie IBM, NCR Corporation und DaimlerChrysler AG umfasste.

**Der CRISP-DM-Leitfaden ist in sechs Phasen unterteilt:**

1. Business Understanding: Verständnis für die geschäftlichen Anforderungen und Ziele  
2. Data Understanding: Verständnis für die verfügbaren Daten und ihre Qualität  
3. Data Preparation: Vorbereitung und Aufbereitung der Daten für die Analyse  
4. Modeling: Auswahl und Anwendung von Data-Mining-Techniken und -Modellen  
5. Evaluation: Bewertung der Modelle in Bezug auf ihre Effektivität und Geschäftsnutzen  
6. Deployment: Implementierung der Modelle in die geschäftliche Praxis  

Dieser Leitfaden hat sich als sehr nützlich und anwendungsorientiert erwiesen und wird häufig in der Industrie sowie im akademischen Bereich verwendet. Er bietet eine strukturierte Herangehensweise, um Data-Mining-Projekte effizient und effektiv zu managen.

Jede dieser Phasen wird in diesem Bericht ausführlich behandelt, um einen ganzheitlichen Überblick und fundierte Schlussfolgerungen zu ermöglichen.


# 2. Data Understanding

## 2.1 Einführung in den HR_Analytics-Datensatz

Der HR_Analytics-Datensatz ist eine reichhaltige Informationsquelle, welcher eine Vielzahl von Datenpunkten zur Belegschaft eines Unternehmens enthält. Dieser Datensatz ist für das Human Resource Management wichtig, da er einen detaillierten Einblick in verschiedene Aspekte des Mitarbeiterlebenszyklus gewährt. Das Spektrum der Variablen reicht von grundlegenden demografischen Informationen wie Alter ("Age") und Geschlecht ("Gender") bis hin zu komplexeren Metriken wie die Zufriedenheit mit der Arbeitsumgebung ("EnvironmentSatisfaction) und der Anzahl der Jahre im Unternehmen("YearsAtCompany").

Der zur Verfügung stehende Datensatz umfasst 38 Spalten und 1481 Zeilen.  
  
Es steht unter:  
<https://www.kaggle.com/datasets/paramitasen/powerbiproject?resource=download> zur Verfügung.  

Benutzt wird die CSV-Datei HR_Analytics unter:  
<https://www.kaggle.com/datasets/paramitasen/powerbiproject?resource=download&select=HR_Analytics.csv>.

Der Datensatz dient als Grundlage für eine breite Palette von Analysen, mit dem Ziel, die innerbetrieblichen Dynamiken besser zu verstehen. Zum Beispiel können die Daten genutzt werden, um herauszufinden, welche Faktoren die Fluktuation ("Attrition") beeinflussen oder wie sich die Entfernung zum Heim ("DistanceFromHome") auf die Zufriedenheit der Mitarbeiter auswirkt. Solche Erkenntnisse sind nicht nur für die akademische Forschung wertvoll, sondern auch für praktizierende HR-Manager, die darauf angewiesen sind, fundierte Entscheidungen auf der Grundlage solider Daten zu treffen.

Die Datenquelle könnte aus einem unternehmensinternen HR-Management-System stammen oder durch spezialisierte Umfragen und Mitarbeiterbefragungen erhoben worden sein. Die Strukturierung dieser Daten erfolgt in der Regel so, dass sie für maschinelles Lernen und fortgeschrittene statistische Analysen geeignet sind.

Zunächst importieren wir die Daten in R und nutzen die readr-Bibliothek:


```r
HR_Analytics <-read_csv("HR_Analytics.csv")
```

Um die Daten zu betrachten, verwenden wir die head()-Funktion:


```r
head(HR_Analytics)
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["EmpID"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Age"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["AgeGroup"],"name":[3],"type":["chr"],"align":["left"]},{"label":["Attrition"],"name":[4],"type":["chr"],"align":["left"]},{"label":["BusinessTravel"],"name":[5],"type":["chr"],"align":["left"]},{"label":["DailyRate"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["Department"],"name":[7],"type":["chr"],"align":["left"]},{"label":["DistanceFromHome"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["Education"],"name":[9],"type":["dbl"],"align":["right"]},{"label":["EducationField"],"name":[10],"type":["chr"],"align":["left"]},{"label":["EmployeeCount"],"name":[11],"type":["dbl"],"align":["right"]},{"label":["EmployeeNumber"],"name":[12],"type":["dbl"],"align":["right"]},{"label":["EnvironmentSatisfaction"],"name":[13],"type":["dbl"],"align":["right"]},{"label":["Gender"],"name":[14],"type":["chr"],"align":["left"]},{"label":["HourlyRate"],"name":[15],"type":["dbl"],"align":["right"]},{"label":["JobInvolvement"],"name":[16],"type":["dbl"],"align":["right"]},{"label":["JobLevel"],"name":[17],"type":["dbl"],"align":["right"]},{"label":["JobRole"],"name":[18],"type":["chr"],"align":["left"]},{"label":["JobSatisfaction"],"name":[19],"type":["dbl"],"align":["right"]},{"label":["MaritalStatus"],"name":[20],"type":["chr"],"align":["left"]},{"label":["MonthlyIncome"],"name":[21],"type":["dbl"],"align":["right"]},{"label":["SalarySlab"],"name":[22],"type":["chr"],"align":["left"]},{"label":["MonthlyRate"],"name":[23],"type":["dbl"],"align":["right"]},{"label":["NumCompaniesWorked"],"name":[24],"type":["dbl"],"align":["right"]},{"label":["Over18"],"name":[25],"type":["chr"],"align":["left"]},{"label":["OverTime"],"name":[26],"type":["chr"],"align":["left"]},{"label":["PercentSalaryHike"],"name":[27],"type":["dbl"],"align":["right"]},{"label":["PerformanceRating"],"name":[28],"type":["dbl"],"align":["right"]},{"label":["RelationshipSatisfaction"],"name":[29],"type":["dbl"],"align":["right"]},{"label":["StandardHours"],"name":[30],"type":["dbl"],"align":["right"]},{"label":["StockOptionLevel"],"name":[31],"type":["dbl"],"align":["right"]},{"label":["TotalWorkingYears"],"name":[32],"type":["dbl"],"align":["right"]},{"label":["TrainingTimesLastYear"],"name":[33],"type":["dbl"],"align":["right"]},{"label":["WorkLifeBalance"],"name":[34],"type":["dbl"],"align":["right"]},{"label":["YearsAtCompany"],"name":[35],"type":["dbl"],"align":["right"]},{"label":["YearsInCurrentRole"],"name":[36],"type":["dbl"],"align":["right"]},{"label":["YearsSinceLastPromotion"],"name":[37],"type":["dbl"],"align":["right"]},{"label":["YearsWithCurrManager"],"name":[38],"type":["dbl"],"align":["right"]}],"data":[{"1":"RM297","2":"18","3":"18-25","4":"Yes","5":"Travel_Rarely","6":"230","7":"Research & Development","8":"3","9":"3","10":"Life Sciences","11":"1","12":"405","13":"3","14":"Male","15":"54","16":"3","17":"1","18":"Laboratory Technician","19":"3","20":"Single","21":"1420","22":"Upto 5k","23":"25233","24":"1","25":"Y","26":"No","27":"13","28":"3","29":"3","30":"80","31":"0","32":"0","33":"2","34":"3","35":"0","36":"0","37":"0","38":"0"},{"1":"RM302","2":"18","3":"18-25","4":"No","5":"Travel_Rarely","6":"812","7":"Sales","8":"10","9":"3","10":"Medical","11":"1","12":"411","13":"4","14":"Female","15":"69","16":"2","17":"1","18":"Sales Representative","19":"3","20":"Single","21":"1200","22":"Upto 5k","23":"9724","24":"1","25":"Y","26":"No","27":"12","28":"3","29":"1","30":"80","31":"0","32":"0","33":"2","34":"3","35":"0","36":"0","37":"0","38":"0"},{"1":"RM458","2":"18","3":"18-25","4":"Yes","5":"Travel_Frequently","6":"1306","7":"Sales","8":"5","9":"3","10":"Marketing","11":"1","12":"614","13":"2","14":"Male","15":"69","16":"3","17":"1","18":"Sales Representative","19":"2","20":"Single","21":"1878","22":"Upto 5k","23":"8059","24":"1","25":"Y","26":"Yes","27":"14","28":"3","29":"4","30":"80","31":"0","32":"0","33":"3","34":"3","35":"0","36":"0","37":"0","38":"0"},{"1":"RM728","2":"18","3":"18-25","4":"No","5":"Non-Travel","6":"287","7":"Research & Development","8":"5","9":"2","10":"Life Sciences","11":"1","12":"1012","13":"2","14":"Male","15":"73","16":"3","17":"1","18":"Research Scientist","19":"4","20":"Single","21":"1051","22":"Upto 5k","23":"13493","24":"1","25":"Y","26":"No","27":"15","28":"3","29":"4","30":"80","31":"0","32":"0","33":"2","34":"3","35":"0","36":"0","37":"0","38":"0"},{"1":"RM829","2":"18","3":"18-25","4":"Yes","5":"Non-Travel","6":"247","7":"Research & Development","8":"8","9":"1","10":"Medical","11":"1","12":"1156","13":"3","14":"Male","15":"80","16":"3","17":"1","18":"Laboratory Technician","19":"3","20":"Single","21":"1904","22":"Upto 5k","23":"13556","24":"1","25":"Y","26":"No","27":"12","28":"3","29":"4","30":"80","31":"0","32":"0","33":"0","34":"3","35":"0","36":"0","37":"0","38":"0"},{"1":"RM973","2":"18","3":"18-25","4":"No","5":"Non-Travel","6":"1124","7":"Research & Development","8":"1","9":"3","10":"Life Sciences","11":"1","12":"1368","13":"4","14":"Female","15":"97","16":"3","17":"1","18":"Laboratory Technician","19":"4","20":"Single","21":"1611","22":"Upto 5k","23":"19305","24":"1","25":"Y","26":"No","27":"15","28":"3","29":"3","30":"80","31":"0","32":"0","33":"5","34":"4","35":"0","36":"0","37":"0","38":"0"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

Das Ergebnis liefert eine formatierte Tabelle der ersten sechs Zeilen des "HR_Analytics"-Datensatzes. Dadurch bekommen wir einen ersten Eindruck von den Daten bevor man die eigentliche Analyse beginnt. 


Der Datensatz hat **1480** Zeilen und **38** Spalten. Die Daten sind bereits *tidy*, das bedeutet:

1. Jede Variable bildet eine Spalte.
2. Jede Beobachtung bildet eine Zeile.
3. Jeder Zellwert repräsentiert eine Messung oder ein Merkmal.

Jede Zeile in der **HR_Analytics**-Tabelle repräsentiert einen individuellen Mitarbeiter innerhalb der Organisation, aus der die Daten stammen. Die Werte in den Spalten für jede Zeile bieten spezifische Informationen über den jeweiligen Mitarbeiter. 

Es ist wichtig zu erwähnen, dass der Datensatz zunächst einer explorativen Datenanalyse (EDA) unterzogen wurde. Dabei wurde festgestellt, dass 57 Einträge in der letzten Spalte Nullwerte aufweisen und dass es einige doppelte Einträge in der Spalte "employeeID" gibt. Diese Unregelmäßigkeiten wurden in der Datenaufbereitungsphase bereinigt.



## 2.2 Bezug zu PowerBI

Der Datensatz wird hauptsächlich verwendet, um ein Dashboard in PowerBI zu erstellen. Das Ziel ist, die Arbeitsabläufe im Unternehmen besser zu verstehen. Wir können z.B. schauen, warum Mitarbeiter gehen oder wie glücklich sie sind, wenn ihr Arbeitsplatz weit von ihrem Zuhause entfernt ist. Diese Infos sind wichtig für die Leute im Personalbereich des Unternehmens, um kluge Entscheidungen zu treffen.

Die Daten können von der Personalabteilung des Unternehmens oder aus Mitarbeiterumfragen kommen. Sie sind so aufgebaut, dass sie auch für komplexe Analysen und Computerprogramme gut zu nutzen sind.

Auch wenn wir den Datensatz hauptsächlich für ein PowerBI-Dashboard verwenden, passt er gut in den Ablauf des CRISP-DM-Modells. Das ist eine Methode, um Daten systematisch zu verstehen und zu nutzen. Besonders in der Phase, in der wir die Daten erst verstehen müssen, hilft uns dieser Datensatz dabei, das Problem, das wir lösen wollen, besser zu begreifen.



## 2.3 Beschreibung der Daten

Die Variablen im Datensatz bieten die Möglichkeit, komplexe Beziehungen und Muster zu erkennen, die für das Personalmanagement von entscheidender Bedeutung sein kann. Beispielsweise könnte eine gute Work-Life-Balance mit einer hohen Arbeitszufriedenheit korrelieren, was wiederum Auswirkungen auf die Mitarbeiterfluktuation haben könnte.

In der zweiten Phase "Data Understanding" soll ein tiefes Verständnis der Variablen und ihrer Bedeutung gelegt werden, um den Grundstein für die späteren Schritte des Data-Mining-Prozesses, insbesondere für die Datenaufbereitung und Modellierung, behandelt werden. 

Die Variablen haben folgende Bedeutungen:





```r
print(variable_definitions, n = Inf)
```

```
## # A tibble: 38 × 3
##    Variable                 Typ             Bedeutung                           
##    <chr>                    <chr>           <chr>                               
##  1 EmpID                    integer (int)   Mitarbeiter-ID                      
##  2 Age                      double (dbl)    Alter                               
##  3 AgeGroup                 character (chr) Altersgruppe                        
##  4 Attrition                character (chr) Fluktuation                         
##  5 BusinessTravel           character (chr) Geschäftsreisen                     
##  6 DailyRate                double (dbl)    Tagesrate                           
##  7 Department               character (chr) Abteilung                           
##  8 DistanceFromHome         double (dbl)    Entfernung zum Heim                 
##  9 Education                integer (int)   Bildungsgrad                        
## 10 EducationField           character (chr) Bildungsfeld                        
## 11 EmployeeCount            integer (int)   Mitarbeiteranzahl                   
## 12 EmployeeNumber           integer (int)   Mitarbeiternummer                   
## 13 EnvironmentSatisfaction  integer (int)   Zufriedenheit mit der Arbeitsumgebu…
## 14 Gender                   character (chr) Geschlecht                          
## 15 HourlyRate               double (dbl)    Stundenlohn                         
## 16 JobInvolvement           integer (int)   Arbeitsbeteiligung                  
## 17 JobLevel                 integer (int)   Joblevel                            
## 18 JobRole                  character (chr) Jobrolle                            
## 19 JobSatisfaction          integer (int)   Jobzufriedenheit                    
## 20 MaritalStatus            character (chr) Familienstand                       
## 21 MonthlyIncome            double (dbl)    Monatliches Einkommen               
## 22 SalarySlab               character (chr) Gehaltsstufe                        
## 23 MonthlyRate              double (dbl)    Monatliche Rate                     
## 24 NumCompanies             integer (int)   Anzahl der Unternehmen              
## 25 Over18                   character (chr) Über 18                             
## 26 OverTime                 character (chr) Überstunden                         
## 27 PercentSalaryHike        double (dbl)    Prozentuale Gehaltserhöhung         
## 28 PerformanceRating        integer (int)   Leistungsbewertung                  
## 29 RelationshipSatisfaction integer (int)   Zufriedenheit in der Beziehung      
## 30 StandardHours            integer (int)   Standardarbeitsstunden              
## 31 StockOptionLevel         integer (int)   Aktienoptionslevel                  
## 32 TotalWorkingYears        double (dbl)    Gesamtzahl der Arbeitsjahre         
## 33 TrainingTimesLastYear    integer (int)   Trainingszeiten im letzten Jahr     
## 34 WorkLifeBalance          integer (int)   Work-Life-Balance                   
## 35 YearsAtCompany           double (dbl)    Jahre im Unternehmen                
## 36 YearsInCurrentRole       double (dbl)    Jahre in aktueller Rolle            
## 37 YearsSinceLastPromotion  double (dbl)    Jahre seit letzter Beförderung      
## 38 YearsWithCurrManager     double (dbl)    Jahre mit aktuellem Manager
```


Zunächst verschaffen wir uns einen Überblick über die Daten.


```r
HR_Analytics %>% describe_tbl()
```

```
## 1 480 (1.5k) observations with 38 variables
## 57 observations containing missings (NA)
## 1 variables containing missings (NA)
## 3 variables with no variance
```
1. Im Datensatz gibt es 1480 Instanzen (Beobachtungen) mit 38 Variablen.
2. 57 Beobachtungen enthalten fehlende Werte (NA).
3. 1 Variable enthält fehlende Werte (NA)
4. 3 Variablen ohne Varianz.

Um diese Daten werden wir uns kümmern müssen.

Es ist wichtig, die Datenklassen (data types) und ihrem Datensatz zu kennen, da sie die Art der Operationen und Analysen bestimmen, die mit diesen Daten durchgeführt werden können. 
Obwohl die Datenklappsen bereits durch die head-Funktion sichtbar gemacht wurden, werden sie hier noch einmal hier explizit dargestellt:


```r
data_classes <- data.frame(Variable = names(HR_Analytics),
                           Class = sapply(HR_Analytics, class))
print(data_classes)
```

```
##                                          Variable     Class
## EmpID                                       EmpID character
## Age                                           Age   numeric
## AgeGroup                                 AgeGroup character
## Attrition                               Attrition character
## BusinessTravel                     BusinessTravel character
## DailyRate                               DailyRate   numeric
## Department                             Department character
## DistanceFromHome                 DistanceFromHome   numeric
## Education                               Education   numeric
## EducationField                     EducationField character
## EmployeeCount                       EmployeeCount   numeric
## EmployeeNumber                     EmployeeNumber   numeric
## EnvironmentSatisfaction   EnvironmentSatisfaction   numeric
## Gender                                     Gender character
## HourlyRate                             HourlyRate   numeric
## JobInvolvement                     JobInvolvement   numeric
## JobLevel                                 JobLevel   numeric
## JobRole                                   JobRole character
## JobSatisfaction                   JobSatisfaction   numeric
## MaritalStatus                       MaritalStatus character
## MonthlyIncome                       MonthlyIncome   numeric
## SalarySlab                             SalarySlab character
## MonthlyRate                           MonthlyRate   numeric
## NumCompaniesWorked             NumCompaniesWorked   numeric
## Over18                                     Over18 character
## OverTime                                 OverTime character
## PercentSalaryHike               PercentSalaryHike   numeric
## PerformanceRating               PerformanceRating   numeric
## RelationshipSatisfaction RelationshipSatisfaction   numeric
## StandardHours                       StandardHours   numeric
## StockOptionLevel                 StockOptionLevel   numeric
## TotalWorkingYears               TotalWorkingYears   numeric
## TrainingTimesLastYear       TrainingTimesLastYear   numeric
## WorkLifeBalance                   WorkLifeBalance   numeric
## YearsAtCompany                     YearsAtCompany   numeric
## YearsInCurrentRole             YearsInCurrentRole   numeric
## YearsSinceLastPromotion   YearsSinceLastPromotion   numeric
## YearsWithCurrManager         YearsWithCurrManager   numeric
```

Für eine detailliertere Analyse des Datensatzes, um Datentypen zu erkunden und zu kategorisieren wird der Datensatz mit der Funktion str() dargestellt. Sie bietet eine kompakte Darstellung der internen Struktur an:


```r
str(HR_Analytics)
```

```
## spc_tbl_ [1,480 × 38] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ EmpID                   : chr [1:1480] "RM297" "RM302" "RM458" "RM728" ...
##  $ Age                     : num [1:1480] 18 18 18 18 18 18 18 18 19 19 ...
##  $ AgeGroup                : chr [1:1480] "18-25" "18-25" "18-25" "18-25" ...
##  $ Attrition               : chr [1:1480] "Yes" "No" "Yes" "No" ...
##  $ BusinessTravel          : chr [1:1480] "Travel_Rarely" "Travel_Rarely" "Travel_Frequently" "Non-Travel" ...
##  $ DailyRate               : num [1:1480] 230 812 1306 287 247 ...
##  $ Department              : chr [1:1480] "Research & Development" "Sales" "Sales" "Research & Development" ...
##  $ DistanceFromHome        : num [1:1480] 3 10 5 5 8 1 3 14 22 3 ...
##  $ Education               : num [1:1480] 3 3 3 2 1 3 2 3 1 1 ...
##  $ EducationField          : chr [1:1480] "Life Sciences" "Medical" "Marketing" "Life Sciences" ...
##  $ EmployeeCount           : num [1:1480] 1 1 1 1 1 1 1 1 1 1 ...
##  $ EmployeeNumber          : num [1:1480] 405 411 614 1012 1156 ...
##  $ EnvironmentSatisfaction : num [1:1480] 3 4 2 2 3 4 2 2 4 2 ...
##  $ Gender                  : chr [1:1480] "Male" "Female" "Male" "Male" ...
##  $ HourlyRate              : num [1:1480] 54 69 69 73 80 97 70 33 50 79 ...
##  $ JobInvolvement          : num [1:1480] 3 2 3 3 3 3 3 3 3 3 ...
##  $ JobLevel                : num [1:1480] 1 1 1 1 1 1 1 1 1 1 ...
##  $ JobRole                 : chr [1:1480] "Laboratory Technician" "Sales Representative" "Sales Representative" "Research Scientist" ...
##  $ JobSatisfaction         : num [1:1480] 3 3 2 4 3 4 4 3 3 2 ...
##  $ MaritalStatus           : chr [1:1480] "Single" "Single" "Single" "Single" ...
##  $ MonthlyIncome           : num [1:1480] 1420 1200 1878 1051 1904 ...
##  $ SalarySlab              : chr [1:1480] "Upto 5k" "Upto 5k" "Upto 5k" "Upto 5k" ...
##  $ MonthlyRate             : num [1:1480] 25233 9724 8059 13493 13556 ...
##  $ NumCompaniesWorked      : num [1:1480] 1 1 1 1 1 1 1 1 1 1 ...
##  $ Over18                  : chr [1:1480] "Y" "Y" "Y" "Y" ...
##  $ OverTime                : chr [1:1480] "No" "No" "Yes" "No" ...
##  $ PercentSalaryHike       : num [1:1480] 13 12 14 15 12 15 12 16 19 14 ...
##  $ PerformanceRating       : num [1:1480] 3 3 3 3 3 3 3 3 3 3 ...
##  $ RelationshipSatisfaction: num [1:1480] 3 1 4 4 4 3 3 3 4 4 ...
##  $ StandardHours           : num [1:1480] 80 80 80 80 80 80 80 80 80 80 ...
##  $ StockOptionLevel        : num [1:1480] 0 0 0 0 0 0 0 0 0 0 ...
##  $ TotalWorkingYears       : num [1:1480] 0 0 0 0 0 0 0 0 0 1 ...
##  $ TrainingTimesLastYear   : num [1:1480] 2 2 3 2 0 5 2 4 2 3 ...
##  $ WorkLifeBalance         : num [1:1480] 3 3 3 3 3 4 4 1 2 3 ...
##  $ YearsAtCompany          : num [1:1480] 0 0 0 0 0 0 0 0 0 1 ...
##  $ YearsInCurrentRole      : num [1:1480] 0 0 0 0 0 0 0 0 0 0 ...
##  $ YearsSinceLastPromotion : num [1:1480] 0 0 0 0 0 0 0 0 0 0 ...
##  $ YearsWithCurrManager    : num [1:1480] 0 0 0 0 0 0 0 0 0 0 ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   EmpID = col_character(),
##   ..   Age = col_double(),
##   ..   AgeGroup = col_character(),
##   ..   Attrition = col_character(),
##   ..   BusinessTravel = col_character(),
##   ..   DailyRate = col_double(),
##   ..   Department = col_character(),
##   ..   DistanceFromHome = col_double(),
##   ..   Education = col_double(),
##   ..   EducationField = col_character(),
##   ..   EmployeeCount = col_double(),
##   ..   EmployeeNumber = col_double(),
##   ..   EnvironmentSatisfaction = col_double(),
##   ..   Gender = col_character(),
##   ..   HourlyRate = col_double(),
##   ..   JobInvolvement = col_double(),
##   ..   JobLevel = col_double(),
##   ..   JobRole = col_character(),
##   ..   JobSatisfaction = col_double(),
##   ..   MaritalStatus = col_character(),
##   ..   MonthlyIncome = col_double(),
##   ..   SalarySlab = col_character(),
##   ..   MonthlyRate = col_double(),
##   ..   NumCompaniesWorked = col_double(),
##   ..   Over18 = col_character(),
##   ..   OverTime = col_character(),
##   ..   PercentSalaryHike = col_double(),
##   ..   PerformanceRating = col_double(),
##   ..   RelationshipSatisfaction = col_double(),
##   ..   StandardHours = col_double(),
##   ..   StockOptionLevel = col_double(),
##   ..   TotalWorkingYears = col_double(),
##   ..   TrainingTimesLastYear = col_double(),
##   ..   WorkLifeBalance = col_double(),
##   ..   YearsAtCompany = col_double(),
##   ..   YearsInCurrentRole = col_double(),
##   ..   YearsSinceLastPromotion = col_double(),
##   ..   YearsWithCurrManager = col_double()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

* "spec_tbl_ [1,480 x 38]" bedeutet, dass der Datensatz 1480 Zeilen und 38 Spalten besitzt.
* "(S3: spec_tbl_df/tbl_df/tbl/data.frame)" zeigt die Klassenhierarchie des Objekts an.
* Spalten und ihre Datentypen
* In "attr(*, 'spec')=" steht, welche Art von Information in jeder Spalte der Tabelle steckt.   
  Es hilft dem Computer zu verstehen, wie er die Daten behandeln soll.
* "attr(*, "problems")=<externalptr>" ist wie ein Hinweis, dass es vielleicht Probleme gab, als die      Daten in den Computer geladen wurden.   
  Es sagt aber nicht, welche Probleme das sind. Es ist wie ein Ausrufezeichen, aber ohne weitere         Erklärung.

## 2.4 Erstellen einer Kopie der Rohdaten

Bevor wir mit der detaillierten Datenanalyse beginnen, ist es wichtig, eine Kopie der Rohdaten zu erstellen. Dieser Schritt wird zu Beginn der "Data Understanding"-Phase durchgeführt, um sicherzustellen, dass die ursprünglichen Daten unverändert bleiben. Durch das Anfertigen dieser Kopie erhalten wir ein Backup und einen Referenzpunkt, auf den wir im weiteren Verlauf des Projekts zurückgreifen können.


```r
HR_Analytics_final <- HR_Analytics
```

## 2.5 Fehlende Daten

Um Fehlende Daten bzw. NAs zu finden, wird die Funktion colSums() mit der Funktion is.na() kombiniert:


```r
colSums(is.na(HR_Analytics_final))
```

```
##                    EmpID                      Age                 AgeGroup 
##                        0                        0                        0 
##                Attrition           BusinessTravel                DailyRate 
##                        0                        0                        0 
##               Department         DistanceFromHome                Education 
##                        0                        0                        0 
##           EducationField            EmployeeCount           EmployeeNumber 
##                        0                        0                        0 
##  EnvironmentSatisfaction                   Gender               HourlyRate 
##                        0                        0                        0 
##           JobInvolvement                 JobLevel                  JobRole 
##                        0                        0                        0 
##          JobSatisfaction            MaritalStatus            MonthlyIncome 
##                        0                        0                        0 
##               SalarySlab              MonthlyRate       NumCompaniesWorked 
##                        0                        0                        0 
##                   Over18                 OverTime        PercentSalaryHike 
##                        0                        0                        0 
##        PerformanceRating RelationshipSatisfaction            StandardHours 
##                        0                        0                        0 
##         StockOptionLevel        TotalWorkingYears    TrainingTimesLastYear 
##                        0                        0                        0 
##          WorkLifeBalance           YearsAtCompany       YearsInCurrentRole 
##                        0                        0                        0 
##  YearsSinceLastPromotion     YearsWithCurrManager 
##                        0                       57
```

Es wird angezeigt, wie viele fehlende Werte (NAs) es in jeder Spalte des Datensatzes gibt. In diesem Fall sind für falst alle Spalten die Werte 0, was bedeutet, dass in diesen Spalten keine fehlenden Werte vorhanden sind. Die einzige Ausnahme ist die Spalte "YearsWithCurrManager", in der 57 fehlende Werte angezeigt werden.

Ein solches Ergebnis ist wichtig, um die Qualität des Datensatzes zu beurteilen. Fehlende Werte können die Genauigkeit statistischer Analysen beeinflussen und die Interpretierbarkeit der Ergebnisse erschweren. Hier sind ein paar Punkte, die aus diesem Ergebnis hervorgehen:

### 2.5.2 Keine fehlenden Werte in den meisten Spalten

Fast alle Spalten haben 0 fehlende Werte, was darauf hindeutet, dass der Datensatz ziemlich vollständig ist. Das ist in der Regel ein gutes Zeichen, da es bedeutet, dass keine Imputation (das Ausfüllen fehlender Werte) oder andere Techniken zur Behandlung fehlender Daten erforderlich sind.

### 2.5.3 Fehlende Werte in einer spezifischen Spalte

Die Spalte "YearsWithCurrManager" hat 57 fehlende Werte. Dies könnte bedeuten, dass die Daten für diese Spalte für einige Beobachtungen nicht verfügbar sind. Dies kann je nach dem Kontext des Datensatzes und dem Ziel der Analyse problematisch sein.

Im Kontext Ihrer ersten Theorie zur Jobzufriedenheit wäre die Spalte "YearsWithCurrManager" eventuell relevant, da die Dauer der Zusammenarbeit mit dem aktuellen Manager ein Indikator für Arbeitsbedingungen und Mitarbeiterbeziehungen sein könnte. Fehlende Werte in dieser Spalte könnten daher die Analyse beeinträchtigen, indem sie ein unvollständiges Bild der Jobzufriedenheit zeichnen.

Fehlende Werte in der Spalte könnten bedeuten, dass einige Mitarbeiter vielleicht noch keinen festen Manager haben oder es eine hohe Fluktuation in der Managerposition gibt. Beides könnte sich auf die Jobzufriedenheit auswirken und sollte in der Analyse berücksichtigt werden.

**Fehlende Werte behandeln**

Das Ersetzen der fehlenden Werte durch den Median oder den Mittelwert kann sinnvoll sein, um ein umfassenderes Bild der Jobzufriedenheit zu erhalten. Ob der Median oder der Mittelwert verwendet werden sollte, hängt von der Verteilung der Daten ab:

Mittelwert: Wenn die Daten ziemlich gleichmäßig verteilt sind und keine extremen Ausreißer vorhanden sind, wäre der Mittelwert eine geeignete Methode.

Median: Wenn es extreme Werte oder eine schiefe Verteilung in der Spalte gibt, wäre der Median vorzuziehen.

Bevor Sie sich für eine Methode entscheiden, sollten die Daten genauer analysiert werden. Ein Histogramm oder ein Boxplot könnte hilfreich sein, um die Datenverteilung besser zu verstehen.

**Boxplot erstellen**


```r
ggplot(data = HR_Analytics_final, aes(x = 1, y = YearsWithCurrManager, fill = "skyblue")) +
  geom_boxplot() +
  xlab("") +
  ylab("Jahre mit aktuellem Manager") +
  ggtitle("Boxplot der Jahre mit aktuellem Manager") +
  scale_fill_manual(values = "skyblue") +
  guides(fill = FALSE)
```

```
## Warning: The `<scale>` argument of `guides()` cannot be `FALSE`. Use "none" instead as
## of ggplot2 3.3.4.
## This warning is displayed once every 8 hours.
## Call `lifecycle::last_lifecycle_warnings()` to see where this warning was
## generated.
```

```
## Warning: Removed 57 rows containing non-finite values (`stat_boxplot()`).
```

![](HR_Analytics2_files/figure-html/unnamed-chunk-11-1.png)<!-- -->

Ein Boxplot ist ein grafisches Werkzeug, das die Verteilung einer Datenserie darstellt. Es zeigt den Median, die Quartile und mögliche Ausreißer im Datensatz. In unserem Fall untersuchten wir eine spezielle Spalte, in der die "YearsWithCurrManager" verzeichnet sind. Der Boxplot zeigte, dass der Mittelwert bei 3 Jahren und der Median bei 4 Jahren liegt. Zudem gab es drei Ausreißer bei 15, 16 und 17 Jahren, und der obere Schnurrbart des Boxplots reichte bis zu 13 Jahren.

Die Abzissenwerte zwischen 0.6 und 1.4 sind eine konventionelle Möglichkeit, die Breite der Box darzustellen und nicht mit den eigentlichen Datenwerten zu verwechseln.

Wenn es darum geht, fehlende Daten zu ersetzen, ist es wichtig, den am besten geeigneten Wert zu wählen. Der Mittelwert ist anfällig für Verzerrungen durch Ausreißer, während der Median eine robustere Metrik ist, insbesondere wenn der Datensatz Ausreißer enthält. Im Kontext der vorliegenden Daten und der Ausreißer wäre es daher angebrachter, den Median als Ersatz für fehlende Werte zu verwenden.

Aufgrund der Robustheit gegenüber Ausreißern und der besseren Darstellung der zentralen Tendenz der Daten, wird der Median von 4 Jahren als der geeignetste Wert für die Ersetzung fehlender Daten eingesetzt.

Mit der mutate()-Funktion aus dem dplyr-Paket werden die Daten modifiziert. Mit der Bedingung "is.na(YearsWithCurrManager)" wird festgestellt, ob ein Wert fehlt. Falls er fehlt, wird er durch den Medianwert "4" ersetzt. Andernfalls bleibt der Wert unverändert.


```r
HR_Analytics_final <- HR_Analytics_final %>%
  mutate(YearsWithCurrManager = ifelse(is.na(YearsWithCurrManager), 4, YearsWithCurrManager))
```

Mit colSums() überprüfen wir noch einmal die Ergebnisse:


```r
colSums(is.na(HR_Analytics_final))
```

```
##                    EmpID                      Age                 AgeGroup 
##                        0                        0                        0 
##                Attrition           BusinessTravel                DailyRate 
##                        0                        0                        0 
##               Department         DistanceFromHome                Education 
##                        0                        0                        0 
##           EducationField            EmployeeCount           EmployeeNumber 
##                        0                        0                        0 
##  EnvironmentSatisfaction                   Gender               HourlyRate 
##                        0                        0                        0 
##           JobInvolvement                 JobLevel                  JobRole 
##                        0                        0                        0 
##          JobSatisfaction            MaritalStatus            MonthlyIncome 
##                        0                        0                        0 
##               SalarySlab              MonthlyRate       NumCompaniesWorked 
##                        0                        0                        0 
##                   Over18                 OverTime        PercentSalaryHike 
##                        0                        0                        0 
##        PerformanceRating RelationshipSatisfaction            StandardHours 
##                        0                        0                        0 
##         StockOptionLevel        TotalWorkingYears    TrainingTimesLastYear 
##                        0                        0                        0 
##          WorkLifeBalance           YearsAtCompany       YearsInCurrentRole 
##                        0                        0                        0 
##  YearsSinceLastPromotion     YearsWithCurrManager 
##                        0                        0
```

### 2.5.4 Falsche Werte in spezifischer Spalte

Alle Mitarbeiter arbeiten acht Stunden am Tag (StandardHours), was aber hier mit der Zahl 80 angegeben wurde. Das muß korrigiert werden und auf 8,0 gesetzt werden.

Eine andere Lösung würde keinen Sinn ergeben. 80 Stunden wären zu viel in einer Woche und zu wenig in einem Monat. 


```r
HR_Analytics_final$StandardHours <- 8
```

Um die Änderungen anzuzeigen, wird noch einmal die Spalte mit der head-Funktion angezeigt.


```r
head(HR_Analytics_final$StandardHours)
```

```
## [1] 8 8 8 8 8 8
```


## 2.6 Erste Datenexploration

**Einleitung**

Die Phase des Data Understanding ist ein kritischer Schritt im Datenanalyseprozess. Sie hilft uns, die Qulaität und Struktur unserer Daten zu verstehen und bereitet uns darauf vor, fundierte Entscheidungen für die nachfolgenden Phasen zu treffen. Die erste Datenexploration bietet einen umfassenden Einblick in die Daten und identifiziert potenzielle Herausforderungen, wie fehlende Werte und Ausreißer.

**Warum im Data Understanding?**

Bevor man in tiefgehende Analysen eintaucht, ist es entscheidend, ein klares Verständnis für die Daten zu haben. Eine vorläufige Untersuchung kann uns wesentliche Informtationen liefern, die uns bei der Entscheidung helfen, welche Methoden und Techniken in späteren Phasen angewendet werden sollten. 

### 2.6.1 Die Grundgesamtheit

**Ziel**

Das Ziel dieses ersten Schrittes ist es, einen groben Überblick über den geamten Datensatzu zu erhalten. Dies ist nützlich, um ein erstes Verständnis für die Daten zu bekommen und mögliche Probleme frühzeitig zu erkennen.  

**Vorgehen**

Es wird die "summary"-Funktion auf den gesamten Datensatz "HR_Analytics_final" angewendet. 


```r
summary(HR_Analytics_final)
```

```
##     EmpID                Age          AgeGroup          Attrition        
##  Length:1480        Min.   :18.00   Length:1480        Length:1480       
##  Class :character   1st Qu.:30.00   Class :character   Class :character  
##  Mode  :character   Median :36.00   Mode  :character   Mode  :character  
##                     Mean   :36.92                                        
##                     3rd Qu.:43.00                                        
##                     Max.   :60.00                                        
##  BusinessTravel       DailyRate       Department        DistanceFromHome
##  Length:1480        Min.   : 102.0   Length:1480        Min.   : 1.00   
##  Class :character   1st Qu.: 465.0   Class :character   1st Qu.: 2.00   
##  Mode  :character   Median : 800.0   Mode  :character   Median : 7.00   
##                     Mean   : 801.4                      Mean   : 9.22   
##                     3rd Qu.:1157.0                      3rd Qu.:14.00   
##                     Max.   :1499.0                      Max.   :29.00   
##    Education     EducationField     EmployeeCount EmployeeNumber  
##  Min.   :1.000   Length:1480        Min.   :1     Min.   :   1.0  
##  1st Qu.:2.000   Class :character   1st Qu.:1     1st Qu.: 493.8  
##  Median :3.000   Mode  :character   Median :1     Median :1027.5  
##  Mean   :2.911                      Mean   :1     Mean   :1031.9  
##  3rd Qu.:4.000                      3rd Qu.:1     3rd Qu.:1568.2  
##  Max.   :5.000                      Max.   :1     Max.   :2068.0  
##  EnvironmentSatisfaction    Gender            HourlyRate     JobInvolvement
##  Min.   :1.000           Length:1480        Min.   : 30.00   Min.   :1.00  
##  1st Qu.:2.000           Class :character   1st Qu.: 48.00   1st Qu.:2.00  
##  Median :3.000           Mode  :character   Median : 66.00   Median :3.00  
##  Mean   :2.724                              Mean   : 65.85   Mean   :2.73  
##  3rd Qu.:4.000                              3rd Qu.: 83.00   3rd Qu.:3.00  
##  Max.   :4.000                              Max.   :100.00   Max.   :4.00  
##     JobLevel       JobRole          JobSatisfaction MaritalStatus     
##  Min.   :1.000   Length:1480        Min.   :1.000   Length:1480       
##  1st Qu.:1.000   Class :character   1st Qu.:2.000   Class :character  
##  Median :2.000   Mode  :character   Median :3.000   Mode  :character  
##  Mean   :2.065                      Mean   :2.725                     
##  3rd Qu.:3.000                      3rd Qu.:4.000                     
##  Max.   :5.000                      Max.   :4.000                     
##  MonthlyIncome    SalarySlab         MonthlyRate    NumCompaniesWorked
##  Min.   : 1009   Length:1480        Min.   : 2094   Min.   :0.000     
##  1st Qu.: 2922   Class :character   1st Qu.: 8051   1st Qu.:1.000     
##  Median : 4933   Mode  :character   Median :14220   Median :2.000     
##  Mean   : 6505                      Mean   :14298   Mean   :2.687     
##  3rd Qu.: 8384                      3rd Qu.:20461   3rd Qu.:4.000     
##  Max.   :19999                      Max.   :26999   Max.   :9.000     
##     Over18            OverTime         PercentSalaryHike PerformanceRating
##  Length:1480        Length:1480        Min.   :11.00     Min.   :3.000    
##  Class :character   Class :character   1st Qu.:12.00     1st Qu.:3.000    
##  Mode  :character   Mode  :character   Median :14.00     Median :3.000    
##                                        Mean   :15.21     Mean   :3.153    
##                                        3rd Qu.:18.00     3rd Qu.:3.000    
##                                        Max.   :25.00     Max.   :4.000    
##  RelationshipSatisfaction StandardHours StockOptionLevel TotalWorkingYears
##  Min.   :1.000            Min.   :8     Min.   :0.0000   Min.   : 0.00    
##  1st Qu.:2.000            1st Qu.:8     1st Qu.:0.0000   1st Qu.: 6.00    
##  Median :3.000            Median :8     Median :1.0000   Median :10.00    
##  Mean   :2.709            Mean   :8     Mean   :0.7919   Mean   :11.28    
##  3rd Qu.:4.000            3rd Qu.:8     3rd Qu.:1.0000   3rd Qu.:15.00    
##  Max.   :4.000            Max.   :8     Max.   :3.0000   Max.   :40.00    
##  TrainingTimesLastYear WorkLifeBalance YearsAtCompany   YearsInCurrentRole
##  Min.   :0.000         Min.   :1.000   Min.   : 0.000   Min.   : 0.000    
##  1st Qu.:2.000         1st Qu.:2.000   1st Qu.: 3.000   1st Qu.: 2.000    
##  Median :3.000         Median :3.000   Median : 5.000   Median : 3.000    
##  Mean   :2.798         Mean   :2.761   Mean   : 7.009   Mean   : 4.228    
##  3rd Qu.:3.000         3rd Qu.:3.000   3rd Qu.: 9.000   3rd Qu.: 7.000    
##  Max.   :6.000         Max.   :4.000   Max.   :40.000   Max.   :18.000    
##  YearsSinceLastPromotion YearsWithCurrManager
##  Min.   : 0.000          Min.   : 0.000      
##  1st Qu.: 0.000          1st Qu.: 2.000      
##  Median : 1.000          Median : 3.000      
##  Mean   : 2.182          Mean   : 4.114      
##  3rd Qu.: 3.000          3rd Qu.: 7.000      
##  Max.   :15.000          Max.   :17.000
```

**Interpretation**

Die Ausgabe zeigt grundlegende statistische Kennzahlen für jede Variabe, wie das arithmetische Mittel, Median, Min- und Max-Werte und die Quartile an. Fehlende Daten und NAs sind nicht mehr vorhanden.

**Diskrete Daten**

Diskrete Daten sind oft das Ergebnis einer Zählung. Dadurch können sie nur bestimmte Werte annehmen und sind endlich oder zählbar unendlich. 

Es gibt Variablen, welche nominale oder ordinale Eigenschaften haben. Auch metrische Daten sind dabei. 

Darüber hinaus können für diskrete Daten auch die Häufigkeiten der verschiedenen einzigartigen Werte dargestellt werden.

**Tidy Data**

Der Datensatz hat **1480** Zeilen und **38** Spalten. Die Daten sind bereits *tidy*, das bedeutet:

1. Jede Variable bildet eine Spalte.
2. Jede Beobachtung bildet eine Zeile.
3. Jeder Zellwert repräsentiert eine Messung oder ein Merkmal.

Jede Zeile in der **HR_Analytics**-Tabelle repräsentiert einen individuellen Mitarbeiter innerhalb der Organisation, aus der die Daten stammen. Die Werte in den Spalten für jede Zeile bieten spezifische Informationen über den jeweiligen Mitarbeiter. 

### 2.6.2 Kategorisierung der Daten

Wenn man die Daten sortieren oder eine Rangfolge erstellen kann, sie aber nicht sinnvoll addieren oder subtrahieren kann, handelt es sich wahrscheinlich um ordinale Daten.

Wenn die Daten nur kategorisiert werden können und keine Reihenfolge oder metrische Eigenschaften haben, sind sie nominale Daten.

Wenn man sinnvolle arithmitische Operationen (wie Addition und Subtraktion) auf die Daten anwenden kann, handelt es sich wahrscheinlich um metrische Daten.

Sicherlich kann die Einteilung je nach Kontext variieren, um manchmal können Daten als entweder metrisch oder ordinal betrachtet werden, abhängig von der Forschungsfrage oder Analysemethode.  

Die Kategorisierung von Daten ist nicht immer strikt festgelegt. Sie hängt oft vom Kontext ab. Man könnte das Bildungsniveau als ordinal betrachten, wenn man lediglich daran interessiert ist, ob höhere Bildung mit einem höheren Einkommen korreliert. In einer anderen Analyse könnte man jedoch die Anzahl der Schuljahre als metrische Daten betrachten, wenn man eine genauere Quantifizierung des Zusammenhangs zwischen Bildung und Einkommen anstrebt.  

**Einfachheit oder Genauigkeit**

Für den Anfang könnte man eine vereinfachte Einteilung wählen, um den Analyseprozess zu erleichtern und erste Einblicke zu gewinnen. Die Kategorisierung ist oft eine Frage des praktischen Vorgehens und dient der Einfachheit halber. 

Es ist wichtig zu betonen, dass die anfängliche Entscheidung für eine bestimmt Datenkategorisierung nicht endgültig ist. Je nachdem, welche spezifischen Fragen in späteren Phasen des Projekts aufkommen oder welche spezifischen Analysemethoden angewendet werden sollen, kann eine Neubewertung der Datenart notwendig sein. Dies ist im Laufe der Explorativen Datenanalyse durchaus möglich, insbesondere wenn neue Thesen entwickelt werden.

Die anfängliche Kategorisierung der Daten dient als Ausgangspunkt, der je nach den Bedürfnissen der Thesen flexibel angepasst erden kann. 

**Ordinale Daten**

* **"AgeGroup"**: Altergruppen sind ordinal, da es eine klare und sinnvolle Reihenfolge gibt.
* **"Education"**: Das Bildungsniveau scheint in numerischer Form kategorisiert zu sein, könnte aber eine Reichenfolge haben (z. B. 1 = keine Ausbildung, 2 = Grundschule, usw.).
* **"EnvironmentSatisfaction"**: Zufriedenheit mit der Arbeitsumgebung scheint ordinal zu sein, da sich numerisch kategorisiert und wahrscheinlich sortierbar ist. 
* **"JobInvolvement"**: wird ebenfalls numerisch kategorisiert und ist wahrscheinlich sortierbar.
* **"JobLevel"**: Joblevel könnte auch ordinal sein, da es eine Rangfolge darstellt. 
* **"JobSatisfaction"**: wird ebenfalls numerisch kategorisiert und ist wahrscheinlich sortierbar.
* **"PerformanceRating"**: wird ebenfalls numerisch kategorisiert und ist wahrscheinlich sortierbar.
* **"RelationshipSatisfaction"**: wird ebenfalls numerisch kategorisiert und ist wahrscheinlich sortierbar.
* **"WorkLifeBalance"**: wird ebenfalls numerisch kategorisiert und ist wahrscheinlich sortierbar.

**Nominale Daten**

* **"EmpID"**: Mirarbeiter-ID ist nominal, da sie eine individuelle Kennung oder Reihenfolge ist.
* **"Attrition"**: Abwanderung (ja/Nein) ist eine nominale Kategorie.
* **"BusinessTravel"**: Art der Geschäftsreise ist nominal.
* **"Department"**: Abteilungen sind in der Regel nominal.
* **"Gender"**: Geschlecht ist nominal. 
* **"JobRole"**: Job-Rollen sind nominal.
* **"MaritalStatus"**: Familienstand ist nominal.
* **"Over18"**: Über 18 (Ja/Nein) ist nominal. 
* **"OverTime"**: Überstunden (Ja/Nein) ist nominal.
* **"SalarySlab"**: Gehaltsklasse ist nominal. 

**Metrische Daten**

* **"Age"**: Alter ist ein metrisches Merkmal.
* **"DailyRate"**: Tagesrate ist metrisch.
* **"DistanceFromHome"**: Entfernung von Zuhause ist metrisch.
* **"EmployeeCount"**: Anzahl der Mitarbeiter könnte als metrisch betrachtet werden, obwohl es in diesem Datensatz wahrscheinlich immer 1 ist.
* **"EmployeeNumber"**: Mitarbeiter-Nummer ist eigentlich nominal, da es aber in einer bestimmten Weise vergeben ist, wird es als metrisch betrachtet.
* **"HourlyRate"**: Stundenrate ist metrisch.
* **"MonthlyIncome"**: Monatseinkommen ist metrisch.
* **"MonthlyRate"**: Monatsrate ist metrisch.
* **"NumCompaniesWorked"**: Anzahl der gearbeiteten Unternehmen ist metrisch.
* **"PercentSalaryHike"**: Prozentsatz der Gehaltserhöhung ist metrisch.
* **"StandardHours"**: Standardstunden können als metrisch betrachtet werden. Jeder arbeitet 8 Stunden am Tag.
* **"StockOptionLevel"**: Aktienoptionslevel ist metrisch.
* **"TotalWorkingYears"**: Gesamte Berufsjahre ist metrisch.
* **"TrainingTimesLastYear"**: Trainingszeiten im letzten Jahr ist metrisch.
* **"YearsAtCompany"**: Jahre im Unternehmen ist metrisch.
* **"YearsInCurrentRole"**: Jahre in der aktuellen Rolle ist metrisch.
* **"YearsSinceLastPromotion"**: Jahre seit der letzten Beförderung ist metrisch.
* **"YearsWithCurrManager"**: Jahre mit aktuellem Manager ist metrisch.

## 2.7 Datenqualitätsprüfung

### 2.7.1 Fehlende Werte

Fehlende Daten bzw. NAs oder Nullen sind in Kapitel 2.5 behandelt worden.

### 2.7.2 Dubletten

Der Datensatz kann mit der Funktion duplicated() überprüft werden. Sie gibt einen logischen Vektor zurück, der True für jede Zeile im Datensatz ist, die eine Duplikat der vorhergehenden Zeile ist.


```r
# Überprüfung auf doppelte Zeilen
duplikate <- duplicated(HR_Analytics_final)

# Anzahl der doppelten Zeilen ermitteln
anzahl_duplikate <- sum(duplikate)

# Ausgabe der Anzahl der doppelten Zeilen
print(paste("Anzahl der doppelten Zeilen: ", anzahl_duplikate))
```

```
## [1] "Anzahl der doppelten Zeilen:  7"
```
Die Anzahl der doppelten Zeilen ist 7. 

Mit dem Ausdruck HR_Analytics_final <-[!dublicated(HR_Analytics_final),] wird der Datensatz gefiltert. Nur die Zeilen, für die der logische Vektor "TRUE" ist, bleiben im Datensatz erhalten. 


```r
# Entfernen der doppelten Zeilen
HR_Analytics_final <- HR_Analytics_final[!duplicated(HR_Analytics_final), ]
```

Nun wird noch einmal auf Dubletten überprüft:


```r
# Überprüfung auf doppelte Zeilen
duplikate <- duplicated(HR_Analytics_final)

# Anzahl der doppelten Zeilen ermitteln
anzahl_duplikate <- sum(duplikate)

# Ausgabe der Anzahl der doppelten Zeilen
print(paste("Anzahl der doppelten Zeilen: ", anzahl_duplikate))
```

```
## [1] "Anzahl der doppelten Zeilen:  0"
```

Keine Dubletten mehr vorhanden.

### 2.7.3 Outliers (Ausreißer)

Die Identifizierung und Behandlung von Ausreißern ist ein wichtiger Schritt in der Datenanalyse. Es soll entschieden werden, ob diese entfernt, transformiert oder beibehalten werden sollen. In R gibt es verschiedene Methoden, um Ausßreißer zu identifizieren und zu behandeln.

Um Ausreißer zu identifizieren können Boxplots oder Scatterplots erstellt werden.

**Warum ein Boxplot weniger hilfreich ist**

Ein Boxplot kann zwar Ausreißer in den Daten anzeigen, jedoch nur im Kontext der Variable selbst. Er zeigt nicht, wie diese Ausreißer im Kontext anderer Variablen stehen. Deshalb könnte es weniger informativ sein, wenn die Beziehungen zwischen mehreren Variablen untersucht werden sollen. Hier könnten Scatterplots, die zwei Variablen miteinander vergleichen, nützlicher sein.

Für den Vergleich wurde sich für die Variable **"MonthlyIncome"** aus mehreren Gründen entschieden:

* Durch die **Variabilität** der Gehälter können sie eine große Bandbreite abdecken. Von Einsteigerpositionen bis hin zu Führungspositionen. Diese große Bandbreite kann dazu führen, dass extreme Werte eher auftreten. 
* Gehälter sind oft eng mit anderen Variablen verbunden und haben daher **Einfluss auf andere Variablen**. Die Variablen wie "JobLevel", "YearsAtCompany", oder "Age" korrelieren. Ausreißer bei "MonthlyIncome" könnten also auf Ausreißer oder Besonderheiten bei anderen Varablen hinweisen.
* Es gibt eine **wirtschaftliche Bedeutung**. Hohe oder niedrige Gehälter können die Interpretation anderer Variablen, wie z. B. "JobSatisfaction". beeinflussen. Ein ungewöhnlich hohes Gehalt könnte beispielsweise eine niedrige Jobzufriedenheit kompensieren.
* Das Gehalt kann durch seine **Komplexität** durch viele verschiedene Faktoren beeinflusst werden, einschließlich Bildung, Erfahrung, Standort, Abteilung usw. Dies macht es zu einer komplexen Variable, die sich gut für die Erkennung von Ausreißern eignet.


**Scatterplots der numerischen Werte**

Die fünf Variablen EmployeeCount, Over18, StandardHours, JobRole und OverTime sollten aus folgenden Gründen ausgeschlossen werden:  
  
  * Eine **geringe Varianz** der Variablen für alle Beobachtungen. Da sie nur einen Wert haben, fügen sie wenig bis keine Information zur Analyse hinzu. Deshalb zeigen die Scatterplots eine Linie oder einen Punkt, was nicht hilfreich ist.
  * Die fünf Variablen sind **irrelevant für die Datenqualitätsprüfung**. Die Variablen haben keinen Einfluss auf die Frage, ob es Ausreißer gibt und ob man sie entfernen oder transformieren sollte.
  * Durch das Entfernen unwichtiger Variabeln wird der Datensatz übersichtlicher und einfacher zu interpretieren, besonders wenn viele Scatterplots erzeugt werden.



```r
# Daten einfügen 
data <- HR_Analytics_final

# Liste der Variablen, die ausgeschlossen werden sollen
exclude_vars <- c("EmployeeCount", "Over18", "StandardHours", "JobRole", "OverTime")

# Liste der numerischen Variablen (ohne MonthlyIncome und ohne auszuschließende Variablen)
numerical_vars <- setdiff(names(data), c("MonthlyIncome", exclude_vars))
numerical_vars <- numerical_vars[sapply(data[, numerical_vars], is.numeric)]

# Entfernen von NA-Werten aus numerical_vars
numerical_vars <- numerical_vars[!is.na(numerical_vars)]

# Teilen Sie die numerischen Variablen in Gruppen zu je zwei Plots auf
groups <- split(numerical_vars, ceiling(seq_along(numerical_vars)/2))

# Erstellen und speichern Sie die Scatterplots
plots <- lapply(groups, function(vars) {
  scatterplots <- lapply(vars, function(var) {
    if (!is.na(var) && !is.null(var) && var != "") { # Bedingung hinzugefügt
      ggplot(data, aes(x = !!sym(var), y = MonthlyIncome)) +
        geom_point(color = "skyblue") +
        labs(x = var, y = "MonthlyIncome") +
        theme_minimal() +
        theme(legend.position = "none")  
    }
  })
  # Entfernen Sie NULL-Elemente aus der Liste
  scatterplots <- Filter(Negate(is.null), scatterplots)
  
  do.call(grid.arrange, c(scatterplots, ncol = 2))
})
```

![](HR_Analytics2_files/figure-html/unnamed-chunk-20-1.png)<!-- -->![](HR_Analytics2_files/figure-html/unnamed-chunk-20-2.png)<!-- -->![](HR_Analytics2_files/figure-html/unnamed-chunk-20-3.png)<!-- -->![](HR_Analytics2_files/figure-html/unnamed-chunk-20-4.png)<!-- -->![](HR_Analytics2_files/figure-html/unnamed-chunk-20-5.png)<!-- -->![](HR_Analytics2_files/figure-html/unnamed-chunk-20-6.png)<!-- -->![](HR_Analytics2_files/figure-html/unnamed-chunk-20-7.png)<!-- -->![](HR_Analytics2_files/figure-html/unnamed-chunk-20-8.png)<!-- -->![](HR_Analytics2_files/figure-html/unnamed-chunk-20-9.png)<!-- -->![](HR_Analytics2_files/figure-html/unnamed-chunk-20-10.png)<!-- -->![](HR_Analytics2_files/figure-html/unnamed-chunk-20-11.png)<!-- -->![](HR_Analytics2_files/figure-html/unnamed-chunk-20-12.png)<!-- -->


### 2.7.4 Inkonsistente Daten

Nach folgenden Sachen wurde bereits überprüft oder ist obsolet:

* Es gibt keine fehlenden Daten mehr in dem Datensatz HR_Analytics_final. Die Daten sind valide.
* Es gibt keine NAs mehr im Datensatz HR_Analytics_final.
* Es gibt keine Variable mit Datumsangaben. Das Überprüfen ist obsolet.
* Es gibt keine unerwarteten Kategorien. Die Daten sind bereinigt.
* Alle numerischen Variablen liegen in einem sinnvollen Bereich.
* Es gibt keine Dubletten.
* Die Datentypen passen zum Datensatz. Dies wurde mit der Funktion str(HR_Analytics_final) überprüft.

**Prüfen auf Texteinheitlichkeit**

Die Überprüfung der Texteinheitlichkeit ist entscheidend für die Qualität und Genauigkeit von Datenanalysen. Inkonsistenzen in Textdaten können zu doppelten Kategorien, ungenauen Aggregationen und fehlerhaften Analysen führen. Text sollte in einem einheitlichen Format sein, um sicherzustellen, dass die Datenanalyse genau ist.

Es werden alle Zeichenketten-Spalten(char_cols) des Datensatzes HR_Analytics_final auf Texteinheitlichkeit überprüft. Dafür wird die Funktion tolower() auf alle Zeichenketten-Variablen angewendet und zeigt die einzigartigen Werte jeder Spalte an.

Die Spalte "EmpID" wird dabei ausgeschlossen. 


```r
# Finden Sie alle charakter-Variablen
char_cols <- names(HR_Analytics_final)[sapply(HR_Analytics_final, is.character)]

# Entfernen Sie 'EmpID' aus der Liste der charakter-Variablen
char_cols <- setdiff(char_cols, "EmpID")

# Wenden Sie 'tolower()' auf alle verbleibenden charakter-Variablen an
HR_Analytics_final[char_cols] <- lapply(HR_Analytics_final[char_cols], tolower)

# Zeigen Sie die einzigartigen Werte jeder verbleibenden charakter-Variablen an
lapply(HR_Analytics_final[char_cols], unique)
```

```
## $AgeGroup
## [1] "18-25" "26-35" "36-45" "46-55" "55+"  
## 
## $Attrition
## [1] "yes" "no" 
## 
## $BusinessTravel
## [1] "travel_rarely"     "travel_frequently" "non-travel"       
## [4] "travelrarely"     
## 
## $Department
## [1] "research & development" "sales"                  "human resources"       
## 
## $EducationField
## [1] "life sciences"    "medical"          "marketing"        "technical degree"
## [5] "other"            "human resources" 
## 
## $Gender
## [1] "male"   "female"
## 
## $JobRole
## [1] "laboratory technician"     "sales representative"     
## [3] "research scientist"        "human resources"          
## [5] "manufacturing director"    "sales executive"          
## [7] "healthcare representative" "research director"        
## [9] "manager"                  
## 
## $MaritalStatus
## [1] "single"   "divorced" "married" 
## 
## $SalarySlab
## [1] "upto 5k" "5k-10k"  "10k-15k" "15k+"   
## 
## $Over18
## [1] "y"
## 
## $OverTime
## [1] "no"  "yes"
```
Durch das Ausschließen von "EmpID" wird sichergestellt, dass die Eindeutigkeit dieser Identifikator-Spalte erhalten bleibt, während der Rest des Datensatzes auf Textkonsistenz überprüft wird.

Die Daten sind standardisiert. Es müssen keine zusätzlichen Zeichen hinzugefügt, oder entfernt werden.

### 2.7.5 Kardinalität

Die Überprüfung der Kardinalität in einem Datensatz bezieht sich auf die Anzahl der einzigartigen Werte, die in jeder Spalte vorhanden sind. Kardinalität ist in vielen Aspekten der Datenanalyse und des Maschinenlernens wichtig:

* Wenn eine Spalte nur wenige einzigartige Werte enthält (z.B. Geschlecht, mit nur den Werten "männlich" und "weiblich"), dann könnte sie als kategorische Variable betrachtet werden. Diese Informationen könnten für die Datenanalyse nützlich sein. Man spricht von einer **geringen Kardinalität**.
* Eine **hohe Kardinalität** ist dann gegeben, wenn eine Spalte eine hohe Anzahl von einzigartigen Werten enthält (z. B. "EmpID"). Diese könnte dann als Identifikator fungieren. Solche Spalten sind oft weniger nützlich für Modelle, die Vorhersagen treffen, aber wichtig für die Datenverknüpfungen oder -identifikation.
* Spalten, welche kategorische als auch kontinuierliche Eigenschaften haben, besitzen eine **mittelgroße Kardinalität** und erfordern eine genauere Untersuchung, um ihre Bedeutung zu verstehen. 

Spalten mit sehr höher Kardinalität können die Leistung von Algorithmen für das Maschinenlernen beeinträchtigen und sind oft schwer interpretierbar. Die Kardinalität kann dazu verwendet werden, um neue Merkmale zu erstellen, die das Modell verbessern können.



```r
# Entfernen Sie 'EmpID' aus der Liste der Spalten
cols_to_check <- setdiff(names(HR_Analytics_final), "EmpID")

# Überprüfen Sie die Kardinalität jeder Spalte
kardinalitaet <- sapply(HR_Analytics_final[cols_to_check], function(col) length(unique(col)))

# Anzeigen der Kardinalität jeder Spalte
print(kardinalitaet)
```

```
##                      Age                 AgeGroup                Attrition 
##                       43                        5                        2 
##           BusinessTravel                DailyRate               Department 
##                        4                      886                        3 
##         DistanceFromHome                Education           EducationField 
##                       29                        5                        6 
##            EmployeeCount           EmployeeNumber  EnvironmentSatisfaction 
##                        1                     1470                        4 
##                   Gender               HourlyRate           JobInvolvement 
##                        2                       71                        4 
##                 JobLevel                  JobRole          JobSatisfaction 
##                        5                        9                        4 
##            MaritalStatus            MonthlyIncome               SalarySlab 
##                        3                     1349                        4 
##              MonthlyRate       NumCompaniesWorked                   Over18 
##                     1427                       10                        1 
##                 OverTime        PercentSalaryHike        PerformanceRating 
##                        2                       15                        2 
## RelationshipSatisfaction            StandardHours         StockOptionLevel 
##                        4                        1                        4 
##        TotalWorkingYears    TrainingTimesLastYear          WorkLifeBalance 
##                       40                        7                        4 
##           YearsAtCompany       YearsInCurrentRole  YearsSinceLastPromotion 
##                       37                       19                       16 
##     YearsWithCurrManager 
##                       18
```

Die Überprüfung der Kardinalität ist ein wichtiger Schritt, um die Struktur des Datensatzes zu verstehen. Sie kann helfen, informierte Entscheidungen über die Datenvorbereitung, das Feature Engineering und die Modellierung zu treffen. Sie sollte auch im Kontext der erwarteten Daten betrachtet werden; eine Kardinalität, die viel höher oder niedriger ist als erwartet, könnte ein Anzeichen für ein Datenqualitätsproblem sein.

Die Kardinalität eines Datensatzes bietet Einblick in die Vielfalt der Werte in jeder Spalte. Beispielsweise zeigt eine Kardinalität von 43 für das Alter an, dass es 43 verschiedene Altersgruppen in diesem Datensatz gibt, was als mittlere Kardinalität betrachtet werden kann. Ebenso weisen Variablen wie Attrition und PerformanceRating mit nur zwei einzigartigen Werten sehr niedrige Kardinalitäten auf und sind wahrscheinlich binäre Merkmale.

Im Gegensatz dazu weisen DailyRate und MonthlyIncome hohe Kardinalitäten auf, was darauf hinweist, dass diese Werte stark variieren und daher als numerische Variablen mit hoher Kardinalität betrachtet werden können. Auf der anderen Seite haben Variablen wie EmployeeCount und Over18 eine Kardinalität von 1, was bedeutet, dass sie für die Analyse möglicherweise nicht sehr informativ. Diese beiden Variablen werden aus HR_Analytics_final entfernt:


```r
# Entfernen der Spalten Over18 und EmployeeCount
HR_Analytics_final <- HR_Analytics_final %>% 
  select(-Over18, -EmployeeCount)
```


Es gibt auch Variablen mit niedriger Kardinalität wie BusinessTravel oder NumCompaniesWorked, die als kategorische Variablen betrachtet werden könnten und möglicherweise durch Techniken wie One-Hot-Encoding in ein format umgewandelt werden könnten, das für maschinelles Lernen besser geeignet ist. Variablen mit hoher Kardinalität, insbesondere Identifikationsvariablen wie EmployeeNumber, könnten nützlich für die Identifikation sein, bieten jedoch für die meisten Arten der statistischen Analyse wahrscheinlich keinen Mehrwert.
