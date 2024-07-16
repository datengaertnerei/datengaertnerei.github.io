---
title: "GenAI und Testen"
excerpt_separator: "<!--more-->"
categories:
  - Misc
tags:
  - test data
---
Ich bin absolut talentfrei bei Illustrationen. Und ich habe mir nie die Mühe gemacht, das richtig zu lernen. Manchmal wäre es aber praktisch, wenn ich dazu niemand anderes bräuchte. Aus diesem Kontext bin ich in dem GenAI Hype losgezogen, um mit Bildgeneratoren zu experimentieren. Und wie meistens in solchen Fällen wollte ich auch hinter die Kulissen schauen. Dazu habe ich mir [FastSD CPU](https://github.com/rupeshs/fastsdcpu) ausgesucht und lokal installiert.

![Screenshot Fast SD](/assets/images/FastSD-local.png)

Das Projekt basiert auf [PyTorch](https://pytorch.org/) und [Gradio](https://www.gradio.app/). Rupesh Sreeraman hat es unter MIT Lizenz veröffentlicht.

Aber was hat das jetzt mit Testen zu tun? 
--

Zum einen finde ich es interessant zu sehen, mit welchen Methoden GenAI Lösungen getestet werden können. Dazu habe ich bei SaaS kaum Möglichkeiten. Hier liegt das gesamte SUT offen vor mir. Zum anderen kann ich es aber auch selbst nutzen zur Erzeugung von Testdaten. Es kommt nach meiner Erfahrung oft genug vor, dass beim Test auch Bilddaten zur Eingabe verwendet werden. Dabei möchte ich folgende Dinge beachten:

- Keine Copyright Verletzungen
- Keine vertraulichen Daten im Testsystem
- Umgang mit Dubletten
- Nutzerfreundliche Testdaten (nicht schon wieder Martina Mustermann...)

Wer es selbt probieren möchte, kann sich das letzte [Release](https://github.com/rupeshs/fastsdcpu/releases) herunterladen und lokal entpacken. Ich nutze Docker, um eine saubere Umgebung zu bekommen:

~~~ 
FROM python:3.11-slim

RUN apt-get update && apt-get -y upgrade
RUN apt-get install -y libgl1-mesa-dev libglib2.0-0

COPY fastsdcpu .

RUN chmod +x ./install.sh
RUN echo " " | ./install.sh

ENTRYPOINT export GRADIO_SERVER_NAME="0.0.0.0" && export GRADIO_SERVER_PORT=8080 && ./start-webui.sh
~~~ 