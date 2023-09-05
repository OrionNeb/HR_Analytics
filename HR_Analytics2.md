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
ggplot(data = HR_Analytics_final, aes(x = 1, y = YearsWithCurrManager)) +
  geom_boxplot() +
  xlab("") +
  ylab("Jahre mit aktuellem Manager") +
  ggtitle("Boxplot der Jahre mit aktuellem Manager")
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
