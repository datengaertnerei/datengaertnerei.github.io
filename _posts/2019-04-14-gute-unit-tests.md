---
title: "Gute Unit Tests schreiben"
excerpt_separator: "<!--more-->"
categories:
  - Misc
tags:
  - test automation
---

Der Begriff Unit Test wird hier als Synonym für einen automatisierten Komponententest verwendet mit folgendem Grundaufbau:

1. Initialisieren des Ausgangszustands
2. Ausführung der zu testenden Operation
3. Abgleich des Ist-Ergebnis mit einem aus der Spezifikation abgeleiteten Sollwert

Das Ziel dabei ist die Identifikation von Veränderungen im Verhalten des zu testenden Moduls durch einen regelmäßig ausgeführten Regressionstest. Veränderungen der Software bei gleichbleibender Erwartung an das Ergebnis kommen dabei in der Praxis oft vor, z.B. durch interne Optimierungen des Moduls oder Aktualisierung genutzter Bibliotheken. 

Den Grundstein für dieses Vorgehen hat Kent Beck bereits vor 30 Jahren mit seinem Artikel [Simple Smalltalk Testing: With Patterns](https://api.semanticscholar.org/CorpusID:6709430) und dem Test Framework SUnit gelegt.
Etwa 10 Jahre später hat er daraus gemeinsam mit Erich Gamma JUnit für Java entwickelt.
Entsprechende Frameworks existieren mittlerweile für alle gängigen modernen Programmiersprachen.

Testanalyse und -design
--

Da Entwickler beim Aufbau des Unit Test den Quellcode der zu testenden Komponente kennen, bietet sich ein strukturbasierter Test an (auch White-Box Verfahren). Die Testabdeckung wird dann mit Hilfe geeigneter Werkzeuge gemessen.
Dabei helfen Äquivalenzklassenbildung und Grenzwertanalyse zur Ermittlung optimaler Parameter für den Test.

Am Beispiel von JUnit 5 zeigen wir, wie Parameter und Erwartungswerte in einem Unit Test ausgelagert werden.

~~~ java
  @ParameterizedTest
  @CsvFileSource(resources = "testGetPrice.csv", numLinesToSkip = 1)
  void testGetPrice(double expected, int age) {
    assertEquals(expected, classUnderTest.getPrice(age), 0.01D);
  }
~~~ 

Bei der Ausführung wird die folgende CSV Datei eingelesen und für jede Zeile nach der Kopfzeile einmal der Test ausgeführt. 
Die Werte jeder Zeile dienen in der Reihenfolge von Links nach Rechts als Parameter für die Methode. Dabei müssen die Datentypen zusammenpassen.

~~~ csv
expected,age
0.0,13 
5.0,14 
5.0,26 
15.0,27 
15.0,64 
10.0,65
~~~ 

Diese Datei kann nicht nur der Entwickler selbst sondern auch der fachliche Experte mit einer Tabellenkalkulation erstellen.
Das Verfahren eignet sich auch für die Umsetzung eines Entscheidungstabellentests.

Daneben sollte der Unit Test auch die Ausnahmebehandlung bei fehlerhaften Parametern prüfen. 
Solche Fälle werden in der Praxis vorkommen und das Verhalten der Komponente in diesen Fällen sollte daher auch getestet werden.

Kurz und prägnant
--
Testen sie einen Sachverhalt in einem Test!  
Testen sie in einer Testklasse nur eine Komponente!  
Isolieren sie die Komponente falls notwendig mit Mocks und Stubs!  
Vermeiden sie lange und verschachtelte Konstruktionen!  
Testen sie nur Komponenten, für die sich ein Test lohnt!

>Do I have to write a test for everything?  
No, just test everything that could reasonably break.  

*[JUnit FAQ](https://junit.org/junit4/faq.html#best_1)*

Komposition an Stelle von Vererbung
--

Die Konventionen der Softwareentwicklung gelten auch bei Unit Tests. Das gilt nicht nur für die üblichen Vorgaben wie Namenskonventionen, Styleguide etc., sondern auch für allgemeine Anforderungen an gutes Softwaredesign. 
Gerade das Prinzip Komposition an Stelle von Vererbung spielt dabei oft eine große Rolle.
So haben die Entwickler beim Wechsel von JUnit 3 auf 4 aus gutem Grund von Vererbung der TestCase Klasse auf Annotations umgestellt.

Wer also Vererbung nutzt, um allgemeine Hilfsmittel vorzubereiten und zusammenzufassen, wird auch bei Unit Tests relativ schnell mit einem schlecht wartbaren und wenig flexiblem Hierarchiebaum kämpfen, den er nur schwer wieder los wird. Bauen sie lieber isolierte Hilfsklassen, die sie nach Bedarf in ihren Tests verwenden.

Schnell sollen sie sein
--

Das klingt im ersten Moment nach einer Floskel. Natürlich wird niemand für Unit Tests bewusst lange Laufzeiten einplanen. Und was bedeutet schnell denn eigentlich konkret?

> Automatically build the whole system and run all of the tests in ten minutes.

*Kent Beck, Cynthia Andres: Extreme Programming Explained*

Ist ihnen das konkret genug? In zehn Minuten soll der komplette Build Prozess mit allen Unit Tests erledigt sein. Einen Integrationstest schließt das nicht ein. Daraus leiten sich drei Anforderungen ab:

+ Verwenden sie einen vernünftig ausgestatteten Build Server
+ Strukturieren sie den Build wirklich nach Komponenten
+ Sorgen sie für Tempo bei ihren Unit Tests

Wiederholbarkeit
--

Aus der Einteilung als Bestandteil des Build Prozesses ergibt sich die Anforderung an die Wiederholbarkeit.
Das meint auch eine sinnvolle Isolierung des Tests, um Abhängigkeiten z.B. zu bestimmten Datenbeständen zu vermeiden.
Und wiederholen sie die Tests auch wirklich jedes Mal. Das Deaktivieren mit ```@Disabled``` ist zwar möglich, aber meistens nur die Manifestation einer schlechten Ausrede, den Test nicht wieder in Ordnung zu bringen.

Auch Tests haben Fehler
--

Dem Risiko von Fehlern in ihren Unit Tests können sie mit Code Reviews begegnen.
Der Code ihrer Unit Tests wird zwar nicht im Produktionssystem genutzt, erfordert aber die gleiche Sorgfalt.

Auch wenn zu ihrem Entwicklungsteam kein ISTQB zertifizierter Tester gehört, lohnt sich ein Blick in das Foundation Level Curriculum.
Daraus kann das Team auch ein Thema für eine Brown Bag Session ableiten. 
Gute Unit Tests sind ein wesentlicher Bestandteil des Software Qualitätsmanagements.