---
title: "3 große Ereignisse in der Geschichte der Versionsverwaltung"
excerpt_separator: "<!--more-->"
categories:
  - DevOps
tags:
  - version control
  - test automation
---
Versionsverwaltungssysteme sind heute integraler Bestandteil der Softwareentwicklung. Durch sie werden Änderungen nachvollziehbar. Source Code lässt sich konkreten Versionen zuordnen. Das macht sie auch zu einem wichtigen Element des Testprozesses.

2022 feiert das Revision Control System (RCS) 40. Geburtstag. Der in diesem Jahr emeritierte Prof. Walter F. Tichy hat es 1982 veröffentlicht. Etwa 10 Jahre davor entstand das Source Code Control System (SCCS) auf einem IBM Mainframe. Beide sind bis heute nutzbar, spielen in der Praxis aber keine Rolle mehr. Mit dem Concurrent Versions System (CVS) gibt es seit 1986 ein RCS Frontend zum Umgang mit mehreren Dateien in einer Operation und einem Client/Server Modell. Parallel gab es eine Reihe von kommerziellen Produkten, die ebenfalls teilweise noch heute erhältlich sind oder zumindest gepflegt werden.

# Subversion

Im Jahr 2000 veröffentlicht dann CollabNet Subversion als Open Source Versionsverwaltung. Es löste diverse Probleme von CVS und ermöglichte beispielsweise das unkomplizierte Verschieben von Elementen. Als echte Client/Server Anwendung war es gut geeignet für die gemeinsame Arbeit im Team an einer Codebasis. Mit Hilfe von Hooks waren Integrationen in Systeme wie Atlassian Jira möglich, etwa um Änderungen an Tickets zu binden. Dazu gab es einen Migrationspfad von CVS und Erweiterungen für Entwicklungsumgebungen, die die Arbeit mit Subversion erleichtern.

Die umfangreichen Features und geringen Einstiregshürden sorgten für eine relativ schnelle Verbreitung. Laut [Eclipse Survey 2010](https://www.eclipse.org/org/press-release/20100604_survey2010.php) nutzten zum Zeitpunkt der Erhebung fast 60% der Teilnehmer Subversion. Natürlich gab es auch Kritik. Bestimmte Operationen sind vergleichsweise langsam. Und gerade über Internetverbindungen über weitere Strecken kann das die Arbeit deutlich behindern.

# Git

Git ist eine Entwicklung von Linus Torvalds von 2005 und wurde getrieben von seinem Konflikt mit BitKeeper. Wer mehr darüber lesen möchte, bemüht dazu bitte die Suchmaschine der Wahl. Mit dieser freien Open Source Software gibt es einen Paradigmenwechsel hin zu verteilten Repositories und nicht-linearer Entwicklung. Die Verbreitung von git entwickelte sich stetig bis hin zum [StackOverflow Developer Survey 2022](https://survey.stackoverflow.co/2022/#technology-version-control), in dem über 95% der professionellen Entwickler Git Nutzer sind.

Die Arbeitsweise erfordert dabei ein Umdenken. Auch erfahrene Anwender von Subversion oder vergleichbaren kommerziellen Produkten müssen den Umgang lernen. Dem stehen deutliche Vorteile in der Zusammenarbeit von Entwicklungsteams gegenüber. In diesem Kontext entstehen die ersten Systeme, die auf dieser Basis systematische Code Reviews in den Entwicklungsprozess bringen. Und parallel steigt auch die Verbreitung von CI/CD Profukten wie Hudson bzw. Jenkins.

# GitHub

2008 folgt dann mit GitHub (und später GitLab etc.) eine Plattform, die auf Basis von Git Produktivitätsfeatures anbietet. Pull Requests und Forks über eine Weboberfläche heben die Möglichkeiten der Zusammenarbeit an einem Softwareprojekt noch einmal auf eine neue Ebene. Und mit Actions ist CI/CD direkt integriert. So erreicht GitHub bis 2022 über 80 Mio. User weltweit.

# Was hat das mit QA zu tun?

Zuerst einmal gibt es im Test ohne Versionsverwaltung keine stabile Basis. Mit Code Reviews nutzen wir eine wichtige Maßnahme zur konstruktiven Qualitätssicherung. Und spätestens in der Testautomatisierung sollte auch der eigene Code seinen Weg in ein entsprechendes Repository finden. Der beschriebene Fortschritt zeigt dabei, dass wir uns heute gut auf Git konzentrieren können. Wissen über 50 Jahre Geschichte der Versionsverwaltung darf oberflächlich sein. Kenntnisse über den Umgang mit CVS in der täglichen Arbeit haben keine Relevanz mehr.

Ein Grundverständnis für den Umgang mit Git und GitHub ist für jeden erlernbar. Es gibt praktisch keine Einstiegshürden. Und gerade im agilen Kontext als Teil eines Entwicklungsteams hilft dieses Wissen auch QA Experten.