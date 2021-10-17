---
title = "Echte Testdaten"
date: 2019-03-30T10:00:00+01:00
categories:
  - STUGHH
tags:
  - test data
---

Produktionsabzüge enthalten selten gute Testdaten. Sie sind zwar einfach zu realisieren und die Anwender finden ihre gewohnten Daten vor. Wirklich uneingeschränkt sinnvoll ist das Verfahren aber höchstens bei einer Systemmigration. Dort möchte ich ja die vollständige und korrekte Übertragung aller Daten testen.
Für alle anderen Fälle betrachten wir einmal die mit diesem Vorgehen verbundenen Risiken.

Datenschutz & Datensicherheit
- 

Der Bezug zur Datenschutz Grundverordnung ist ja offensichtlich bei personenbezogenen Daten.
Den Schutz von sensiblen Unternehmensdaten berücksichtigen viele aber nicht oder nur unzureichend.
So kann man aus einen Produktionsabzug durchaus die Anlagestrategie eines Fonds nachvollziehen.
Auch die Einkaufspreise eines Handelsunternehmens sind für Mitbewerber wertvoll, ebenso wie 
die Lieferketten und Produktionsplanungsdaten eines Industrieunternehmens.

Nicht umsonst enthält die ISO 27001 von 2013 in A.14.3.1 (Protection of test data) einen eigenen Abschnitt zu Datenschutz und Datensicherheit in Testsystemen. In der Praxis wird ein Testsystem nie so gut gesichert sein wie das Produktionssystem.
Um den Testern ihre Arbeit zu ermöglichen, werden zusätzliche Berechtigungen für Auswertungen geschaffen.
Datentransfers sind oft in deutlich weiterem Umfang erlaubt, z.B. um Werkzeuge für den Datenvergleich zu verwenden.
Und nicht zuletzt sind die Testdaten auch Pflichtbestandteil der Testdokumentation.

Projekterfolg
- 

> Mein Produktionsdatenbestand ist so groß, dass die Kosten für das Testsystem das halbe Projektbudget in Anspruch nehmen.

Und der Produktionsabzug inkl. Nacharbeiten dauert fünf Tage. Das ist auch heute noch Realität in vielen Unternehmen.
Dazu kommt der Umgang mit Regressionstests. Da der Produktionsbestand ständigen Änderungen unterliegt, taugt er nicht als stabile Basis für vordefinierte Regressionstests. Die Testdaten passen nicht mehr zu den erwarteten Ergebnissen.
Das kompensieren viele mit sogenannten Vorher- und Nachherläufen, bei denen direkt nach dem Aufbau des Testsystems ein Verarbeitungsergebnis als korrekt angenommen wird und als Referenz dient. Nach Installation der geänderten Software wird das Ergebnis der wiederholten Verarbeitung mit dem Referenzergebnis verglichen. Das erhöht den Aufwand für Regressionstests und ignoriert bestehende Fehler im Produktionssystem.

Synthetische Testdaten entstehen natürlich auch nicht aus dem Nichts. Der Aufwand für die Gewinnung der Testdaten muss gerechtfertig sein. Dafür sind sie dann maßgeschneidert für den Test und verschwenden keine Systemressourcen.

Testqualität
- 

> Mein Produktionsbestand ist noch sehr klein. Wie kann ich die Skalierbarkeit meiner Software testen?

Wenn Testdaten nicht zu den Aufgaben des Tests passen, kann die gewünschte Qualität der zu testenden Software nicht gewährleistet werden. Die Daten aus einem Produktionsabzug können nicht nur aufwendig zu verarbeiten und zu schützen sein.
Veraltet oder lückenhaft bezogen auf die geplanten Tests sind ebenso mögliche Attribute.
Ein Beispiel dafür ist ein erfolgreiches Startup, das die Skalierbarkeit der eigenen Software mit Bezug auf das aktuelle Kundenwachstum testen möchte.

Mit Testdaten aus dem Produktionssystem werden ich also mit hoher Wahrscheinlichkeit Kompromisse eingehen. 
Sie verleiten in der Praxis oft dazu, sich beim Test auf den [Happy Path](https://de.wikipedia.org/wiki/Testpfad) zu beschränken.
Für den Test des Ausnahmeverhaltens der zu testenden Software sind sie schlicht ungeeignet.
Nachdem jetzt ausreichend dokumentiert ist, wie man es nicht machen sollte, stellt sich die Frage nach einer Lösung.

Der fundamentale TDM-Prozess
-

Der Testdatenmanagement-Prozess (TDM-Prozess) orientiert sich am ISTQB®-Testprozess und besteht aus
den folgenden Aktivitäten:

+ Planung (TDM)  
+ Steuerung (TDM)  
+ Testdaten spezifizieren  
+ Testdatenerzeugung konzipieren  
+ Testdaten bereitstellen  
+ Testdatenabschlussbericht erstellen  
+ Testdaten archivieren  

Der erste konkrete Schritt zu echten Testdaten ist also eine Spezifikation der Anforderungen.
Die erfolgt in erster Linie auf Basis von Testfällen und Szenarien, aus denen diese Anforderungen abgeleitet werden.
Die finanziellen Rahmenbedingungen wirken dabei als Beschränkung.
Aus globalen Anforderungen wie der DS-GVO oder der ISO 27001 Norm ergeben sich zusätzliche Restriktionen.

Lösen sie sich dabei bitte von dem Irrglauben, dass Anforderungsspezifikationen in Form eines Romans geliefert werden. Die Spezifikation sollte so kurz wie möglich in verständlicher Form abgefasst sein.

Testdaten erzeugen
-

Eine wesentliche Frage zu Beginn der Konzeption der Testdatenerzeugung ist: "Können wir ein Testsystem bereitstellen mit produktionsidentischer Konfiguration ohne Stamm- und Bewegungsdaten?"

Ohne diese Möglichkeit beginnt die Bereitstellung des Testsystems mit einem Produktionsabzug mit den notwendigen Nacharbeiten wie Anonymisierung bzw. Pseudonymisierung.
Je nach Möglichkeit und Ressourcenbedarf folgt eine Reduktion des Datenbestands. etwa durch eine Archivierungsfunktion.

Um den oben spezifizierten Anforderungen an Testdaten zu genügen, wird dann zwischen der Selektion bestehender Daten und der Erzeugung synthetischer Daten unterschieden. Die Komplexität des zu testenden Systems bestimmt dabei den Aufwand im Testdatendesign wesentlich.
Testdatengeneratoren erleichtern dann die eigentliche Erzeugung von synthetischen Testdaten. Ein Beispiel dafür findet ihr in meinem [Repository](https://github.com/datengaertnerei/test-data-service "test-data-service").

Die Anforderungen an Datenmengen für einen Test sind in der Regel kleiner als bei Produktionsverfahren. 
Ausnahmen bilden unter anderem spezielle Lasttests wie oben für das Wachstumsszenario beschrieben.
Der Testdatenkoeffizient liefert einen Anhaltspunkt bezüglich der Datensparsamkeit und effizienten Ressourcennutzung.
Er beschreibt das Verhältnis aus vorhandenen zu genutzten Testdaten. Bei 100 GB vorhandenen und 20 GB genutzten Testdaten ist der Koeffizient 20%. 

Häufig bewährt sich eine Mischform aus anonymisierten Testdaten und synthetischen Testdaten.
In jedem Fall soll aber die Entscheidung über die im Test verwendeten Daten bewusst erfolgen auf Basis qualifizierter Anforderungen.