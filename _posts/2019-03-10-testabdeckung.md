---
title: "Die Sache mit der Testabdeckung"
excerpt_separator: "<!--more-->"
categories:
  - Misc
tags:
  - test automation
---
Mit vielen modernen Programmiersprachen ist die Messung der Testabdeckung im Ablauf der Testautomatisierung dank entsprechender Werkzeuge kein Problem.
Bei einen Continuous Integration Aufbau bekommen wir die entsprechenden Berichte regelmäßig öffentlich präsentiert.
Da ist dann häufig der Ruf nach einer Mindestabdeckung nicht weit. Das sieht gut aus, ist einfach zu ermitteln, und vermittelt ein gutes Gefühl.
Aber ist das wirklich ein sinnvolles Qualitätsmerkmal?  

Wir nehmen ein Beispiel: Eine triviale Funktion zur Ermittlung eines Eintrittspreises abhängig vom eingegebenen Alter.  

+ Kinder unter 14 haben freien Eintritt.
+ Ab 14 Jahren ist der Schüler- und Studententarif 5 EUR.
+ Ab 27 Jahren zahlt man 15 EUR regulären Eintritt.
+ Ab 65 Jahren gibt es 10 EUR ermäßigten Preis für Rentner.

Die folgende Implementierung enthält fachliche (und stilistische) Fehler:

~~~ java
public class PriceCalculator {
  public double getPrice(int age) {
    double result = 0.0D;
    if (age < 14) {
      result = 0.0D;
    }
    if (age > 14 && age < 27) {
      result = 5.0D;
    }
    if (age > 27 && age < 65) {
      result = 15.0D;
    }
    if (age > 65) {
      result = 10.0D;
    }
    return result;
  }
}
~~~ 

Der Unit Test mit JUnit läuft aber, ohne die Fehler zu identifizieren. Und er erreicht 100% Testabdeckung. 
Gäste im Alter von 27 oder 65 Jahren haben in der Praxis dann Glück gehabt.
Dieser Test prüft also zum einen nicht die wichtigen Grenzfälle. Er berücksichtigt zum anderen nicht die Verwendung von Äquivalenzklassen. Das Vorgehen ähnelt eher einem Schuss mit einer Schrotladung.

~~~ java
import static org.junit.jupiter.api.Assertions.assertEquals;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

class PriceCalculatorTest {

  PriceCalculator classUnderTest;

  @BeforeEach
  void setUp() throws Exception {
    classUnderTest = new PriceCalculator();
  }

  @Test
  void testGetPrice() {
    assertEquals(0.0D, classUnderTest.getPrice(10), 0.01D);
    assertEquals(5.0D, classUnderTest.getPrice(20), 0.01D);
    assertEquals(15.0D, classUnderTest.getPrice(30), 0.01D);
    assertEquals(15.0D, classUnderTest.getPrice(40), 0.01D);
    assertEquals(15.0D, classUnderTest.getPrice(50), 0.01D);
    assertEquals(15.0D, classUnderTest.getPrice(60), 0.01D);
    assertEquals(10.0D, classUnderTest.getPrice(70), 0.01D);
    assertEquals(10.0D, classUnderTest.getPrice(80), 0.01D);
    assertEquals(10.0D, classUnderTest.getPrice(90), 0.01D);
  }
}
~~~ 

Zuerst bringen wir daher den Test in Ordnung. Die neun gleichförmigen Methodenaufrufe reduzieren wir auf einen Aufruf mit Parametern.
JUnit hat dafür entsprechende Annotationen (hier mit JUnit 5). Die Prüfungen beziehen sich dabei jeweils auf die Altersgrenzen der Preisspannen. Weitere Tests innerhalb dieser Grenzen bringen keinen zusätzlichen Erkenntnisgewinn und sind daher nutzlos.

~~~ java
import static org.junit.jupiter.api.Assertions.assertEquals;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.CsvSource;

class PriceCalculatorTest {

  PriceCalculator classUnderTest;

  @BeforeEach
  void setUp() throws Exception {
    classUnderTest = new PriceCalculator();
  }

  @ParameterizedTest
  @CsvSource({"0.0, 13", "5.0, 14", "5.0,26", "15.0,27", "15.0,64", "10.0,65"})
  void testGetPrice(double expected, int age) {
    assertEquals(expected, classUnderTest.getPrice(age), 0.01D);
  }
}
~~~ 

Da der Test jetzt natürlich Fehler identifiziert, müssen wir nun endlich die Methode zur Preisermittlung korrigieren.
Bei der Gelegenheit ergänzen wir eine Prüfung auf ungültige Altersangaben (Alter kleiner Null). In der Praxis sollten sie natürlich keine RuntimeException direkt in dieser Form werfen.

~~~ java
public class PriceCalculator {
  public double getPrice(int age) {
    if (age < 0) {
      throw new RuntimeException("Age below zero");
    } else if (age < 14) {
      return 0.0D;
    } else if (age < 27) {
      return 5.0D;
    } else if (age < 65) {
      return 15.0D;
    } else { // >= 65
      return 10.0D;
    }
  }
}
~~~

Mit einer kleinen Ergänzung des Tests erreichen wir erneut 100% Testabdeckung.

~~~ java
import static org.junit.jupiter.api.Assertions.assertThrows;
//...
  @Test
  void testGetPriceInvalid() {
    assertThrows(
        RuntimeException.class,
        () -> {
          classUnderTest.getPrice(-1);
        });
  }
~~~ 

Die Messung mit [JaCoCo](https://www.jacoco.org/) bestätigt das.
Aber wir sehen hier eben einen strukturbasierten Test, der keine echte Aussagekraft zur korrekten Umsetzung der Anforderung besitzt.
![100% Code Coverage](/assets/images/DemoCodeCoverage.png)

Das muss jeder verstanden haben, der Kennzahlen auf Basis von Messungen der Testabdeckung im Test setzt.
Ich kann sogar die falschen Anreize setzen durch harte Vorgaben von Prozentwerten.
Das Ergebnis sind dann häufig Testklassen, die inhaltlich nahezu wertlos sind, aber den zu testenden Code möglichst vollständig durchlaufen ohne Fehler zu werfen.

Damit wiege ich aber die Beteiligten in trügerischer Sicherheit. Ich verleite vielleicht sogar zu Refactorings, deren Fehler in der Umsetzung erst im produktiven Umfeld entdeckt werden. Wir sollten also den Werkzeugen nicht mehr Bedeutung zumessen als notwendig.
Wie Fähigkeit des Entwicklungsteams zur Implementierung guter automatisierter Tests und zur Identifikation der Stellen, an denen diese notwendig sind, zählt in der Praxis.