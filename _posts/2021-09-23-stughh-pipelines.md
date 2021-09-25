---
title: "Build-Pipelines und Testen - STUGHH 23.09.2021"
excerpt_separator: "<!--more-->"
categories:
  - STUGHH
tags:
  - pipelines
  - test automation
---

Unser virtuelles [Software-Test User Group Hamburg](https://www.xing.com/communities/groups/software-test-user-group-hamburg-5a87-1002644/posts) Treffen hatte das Thema "Build-Pipelines und Testen". Gemeinsam mit [Andreas Kühl](https://www.xing.com/profile/Andreas_Kuehl) hatte ich das Vergnügen, ein wenig über Erfahrungen mit CI/CD Pipelines zu berichten und mit den Teilnehmern ins Gespräch zu kommen.

Mein Foliensatz findet ihr hier: [Präsentation QA in CI/CD Pipelines (PDF)](/assets/presentations/2021-09-23-qa-in-ci-cd-pipelines.pdf)

#Qualitätskriterien für Pipelines
[Keeping Developers Happy with a Fast CI](https://shopify.engineering/faster-shopify-ci) - Artikel im Shopify Engineering Blog

#Statische Analyse

[SonarQube](https://www.sonarqube.org/) bzw. [SonarCloud](https://sonarcloud.io/) - Verbreitete Software zur statischen Analyse (Open Source & Commercial)
[Wikipedia Liste mit Tools](https://en.wikipedia.org/wiki/List_of_tools_for_static_code_analysis) - Hier wird eigentlich jeder fündig

#Dependency Checks

[OWASP Dependency Check](https://owasp.org/www-project-dependency-check/) - OWASP Tool zur Abgleich von 3rd Party Komponenten mit der National Vulerability Database.
[GitHub Dependabot](https://github.com/dependabot) Alternative von GitHub


#Test Impact Analysis
[The Rise of Test Impact Analysis](https://martinfowler.com/articles/rise-test-impact-analysis.html) - Paul Hammant bei Martin Fowler über TIA.
[Jest Option lastCommit](https://jestjs.io/docs/cli#--lastcommit) - Das JavaScript Test Framework Jest kann einen Lauf auf geänderte Dateien einschränken.


#Weitere QA Komponenten für Pipelines

[ZAP Baseline Scan](https://www.zaproxy.org/docs/docker/baseline-scan/) - OWASP Zed Attack Proxy Scan für übliche Schwachstellen
[Accessibility Check](https://github.com/datengaertnerei/A11yTesting) - Maschinelle Tests auf Barrierefreiheit (mit Pa11y oder Lighthouse)

#Tipp des Tages von Andreas

[JUnit 5 Annotation Type Tag](https://junit.org/junit5/docs/5.0.2/api/org/junit/jupiter/api/Tag.html) - Ermöglicht Traceability und zielgerichtete Testläufe

#Tipp aus dem Publikum

[CodeScene](https://codescene.io/) - Ein neuer Ansatz zur statischen Analyse, der das Verhalten des Team einbezieht
