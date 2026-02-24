---
kernelspec:
  name: python3
  display_name: 'Python 3'
---

# 6.2 Zufallszahlen und Simulation

Kein Fertigungsprozess ist absolut präzise. Ein gefertigter Bolzen, der einen
Solldurchmesser von 25.0 mm haben soll, wird in der Realität mal 24.97 mm, mal
25.04 mm oder 24.98 mm messen. Diese unvermeidliche Streuung ist ein zentrales
Thema in der Qualitätssicherung und der Konstruktion. Um solche Prozesse zu
untersuchen, ohne tatsächlich tausende Bauteile fertigen zu müssen, verwenden
Ingenieurinnen und Ingenieure **Simulationen**. Das Python-Modul `random` stellt
Funktionen zur Verfügung, mit denen wir Zufallszahlen erzeugen und damit solche
Streuprozesse nachbilden können.

## Lernziele

```{admonition} Lernziele
:class: attention
* [ ] Sie können das Modul `random` importieren.
* [ ] Sie können mit `random.uniform()` gleichverteilte Zufallszahlen aus einem
  kontinuierlichen Wertebereich erzeugen.
* [ ] Sie können mit `random.randint()` ganzzahlige Zufallszahlen erzeugen.
* [ ] Sie können mit `random.choice()` ein zufälliges Element aus einer Liste
  auswählen.
* [ ] Sie können Zufallszahlen mit einer for-Schleife kombinieren, um einfache
  Simulationen durchzuführen.
```

## Das Modul random

Das Modul `random` ist Teil der Python-Standardbibliothek und muss nicht
zusätzlich installiert werden. Anders als Plotly Express, das wir mit einem
Alias importiert haben, importieren wir `random` ohne Alias:

```{code-cell} python
import random
```

Danach stehen uns die Funktionen des Moduls über den Modulnamen zur Verfügung,
also zum Beispiel `random.uniform()` oder `random.randint()`.

## Kontinuierliche Zufallszahlen: random.uniform()

Die Funktion `random.uniform(a, b)` erzeugt eine zufällige Fließkommazahl, die
gleichmäßig zwischen `a` und `b` verteilt ist. Das bedeutet: Jeder Wert
innerhalb dieses Bereichs ist gleich wahrscheinlich.

Kehren wir zum Beispiel aus Kapitel 5.8 zurück. Dort haben wir geprüft, ob
Bolzen mit gemessenen Durchmessern innerhalb der Toleranz von 25.0 mm ± 0.3 mm
liegen. Jetzt simulieren wir die Fertigung: Jeder gefertigte Bolzen hat aufgrund
von Fertigungsstreuung einen leicht unterschiedlichen Durchmesser. Wir nehmen
an, dass die Durchmesser gleichmäßig zwischen 24.5 mm und 25.5 mm streuen:

```{code-cell} python
import random

durchmesser = random.uniform(24.5, 25.5)
print(f"Simulierter Durchmesser: {durchmesser:.3f} mm")
```

Jedes Mal, wenn wir diese Zelle ausführen, erhalten wir einen anderen Wert.
Das ist das Wesen einer Zufallszahl.

```{admonition} Mini-Übung
:class: tip
Führen Sie die obige Code-Zelle fünfmal hintereinander aus. Notieren Sie die
erzeugten Werte. Was beobachten Sie? Liegen alle Werte zwischen 24.5 und 25.5?
```

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
Jeder Aufruf von `random.uniform(24.5, 25.5)` erzeugt einen anderen Wert,
aber alle Werte liegen im angegebenen Bereich. Das Ergebnis könnte
beispielsweise so aussehen:

```
Simulierter Durchmesser: 24.823 mm
Simulierter Durchmesser: 25.187 mm
Simulierter Durchmesser: 24.612 mm
Simulierter Durchmesser: 25.341 mm
Simulierter Durchmesser: 24.954 mm
```
````

## Fertigungsprozess simulieren

Ein einzelner Zufallswert ist wenig aussagekräftig. Interessant wird es, wenn
wir viele Bauteile simulieren und auswerten. Wir kombinieren `random.uniform()`
mit einer for-Schleife und knüpfen direkt an das Qualitätsprüf-Beispiel aus
Übung 5.8 an.

Wir simulieren die Fertigung von 200 Bolzen und prüfen für jeden, ob er
innerhalb der Toleranz liegt:

```{code-cell} python
import random
import plotly.express as px

SOLL_MM = 25.0
TOLERANZ_MM = 0.3
GRENZE_UNTEN_MM = SOLL_MM - TOLERANZ_MM
GRENZE_OBEN_MM = SOLL_MM + TOLERANZ_MM
ANZAHL_BOLZEN = 2000

anzahl_iO = 0
anzahl_niO = 0

for i in range(ANZAHL_BOLZEN):
    d = random.uniform(24.5, 25.5) # <-- neu im Vgl. zu Übung 5.8 Simulation
    ist_fehlerhaft = False
    if d < GRENZE_UNTEN_MM:
        ist_fehlerhaft = True
    if d > GRENZE_OBEN_MM:
        ist_fehlerhaft = True
    if ist_fehlerhaft == True:
        anzahl_niO = anzahl_niO + 1
    if ist_fehlerhaft == False:
        anzahl_iO = anzahl_iO + 1

ausschussquote = anzahl_niO / ANZAHL_BOLZEN * 100

print(f"iO-Teile:       {anzahl_iO}")
print(f"niO-Teile:      {anzahl_niO}")
print(f"Ausschussquote: {ausschussquote:.1f} %")

fig = px.bar(x=["iO-Teile", "niO-Teile"],
             y=[anzahl_iO, anzahl_niO],
             labels={"x": "Klassifizierung", "y": "Anzahl Bolzen"},
             title=f"Qualitätsprüfung: Simulation von {ANZAHL_BOLZEN} Bolzen")
fig.show()
```

Da wir Zufallszahlen verwenden, ergibt jede Ausführung ein etwas anderes
Ergebnis. Die Ausschussquote liegt bei einer gleichmäßigen Streuung zwischen
24.5 und 25.5 mm und einer Toleranz von ±0.3 mm theoretisch bei 40 %, da der
zulässige Bereich (0.6 mm) 60 % des Gesamtbereichs (1.0 mm) ausmacht.

```{admonition} Mini-Übung
:class: tip
Ändern Sie die Anzahl der simulierten Bolzen auf 20, 200 und 2000. Was
beobachten Sie bei der Ausschussquote? Warum nähert sich das Ergebnis mit
steigender Anzahl dem theoretischen Wert von 40 % an?
```

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
Bei 20 Bolzen schwankt die Ausschussquote stark, zum Beispiel zwischen 25 % und
55 %. Bei 200 Bolzen ist die Schwankung deutlich geringer, bei 2000 Bolzen
nähert sich das Ergebnis zuverlässig dem theoretischen Wert von 40 %.

Dieses Prinzip nennt man das **Gesetz der großen Zahlen**: Je mehr Versuche
durchgeführt werden, desto stabiler und vorhersehbarer wird das Ergebnis. Das
ist die Grundidee hinter der sogenannten **Monte-Carlo-Simulation**, die in der
Ingenieurpraxis eingesetzt wird, um komplexe Systeme statistisch zu analysieren.
````

## Ganzzahlige Zufallszahlen: random.randint()

Manchmal brauchen wir keine Fließkommazahlen, sondern ganzzahlige Zufallswerte.
Die Funktion `random.randint(a, b)` erzeugt eine zufällige ganze Zahl zwischen
`a` und `b`, wobei beide Grenzen eingeschlossen sind.

Ein klassisches Modell für diskrete Zufallsprozesse ist der Würfelwurf. Mit
`random.randint(1, 6)` simulieren wir das Würfeln:

```{code-cell} python
import random

wurf = random.randint(1, 6)
print(f"Gewürfelt: {wurf}")
```

Mit einer for-Schleife simulieren wir 600 Würfe und zählen, wie oft jede Zahl
gewürfelt wird. Bei einem fairen Würfel erwarten wir jede Zahl ungefähr gleich
häufig, also je ca. 100-mal:

```{code-cell} python
import random
import plotly.express as px

ANZAHL_WUERFE = 600

haeufigkeit = [0, 0, 0, 0, 0, 0]   # Index 0 bis 5 für Augenzahl 1 bis 6

for i in range(ANZAHL_WUERFE):
    wurf = random.randint(1, 6)
    haeufigkeit[wurf - 1] = haeufigkeit[wurf - 1] + 1

fig = px.bar(x=[1, 2, 3, 4, 5, 6],
             y=haeufigkeit,
             labels={"x": "Augenzahl", "y": "Häufigkeit"},
             title=f"Würfelsimulation: {ANZAHL_WUERFE} Würfe")
fig.show()
```

Beachten Sie den Ausdruck `haeufigkeit[wurf - 1]`: Da Python mit Index 0
beginnt, muss die Augenzahl um 1 vermindert werden, um den richtigen Index zu
erhalten. Eine Augenzahl von 1 entspricht also Index 0, eine 6 entspricht
Index 5.

```{admonition} Mini-Übung
:class: tip
Erhöhen Sie die Anzahl der Würfe auf 6000. Vergleichen Sie das Balkendiagramm
mit dem Ergebnis bei 600 Würfen. Was beobachten Sie?
```

````{admonition} Lösung
:class: tip
:class: dropdown
Bei 6000 Würfen sind die Balken deutlich gleichmäßiger als bei 600 Würfen.
Jede Augenzahl erscheint mit einer Häufigkeit nahe 1000 (also ca. 1/6 von
6000). Mit steigender Würfelanzahl wird das Ergebnis stabiler, was wiederum
das Gesetz der großen Zahlen bestätigt.
````

## Zufällige Auswahl: random.choice()

Manchmal möchten wir nicht eine Zahl, sondern ein zufälliges Element aus einer
bestehenden Liste auswählen. Die Funktion `random.choice(liste)` wählt zufällig
ein Element aus der übergebenen Liste aus, wobei jedes Element gleich
wahrscheinlich ist.

In der Fertigung könnte dies zum Beispiel die zufällige Auswahl eines Materials
für den nächsten Fertigungsauftrag sein:

```{code-cell} python
import random

materialien = ["Stahl", "Aluminium", "Titan", "Kupfer"]
auswahl = random.choice(materialien)
print(f"Nächstes Material: {auswahl}")
```

Mit einer Schleife simulieren wir 12 aufeinanderfolgende Fertigungsaufträge und
zählen die Häufigkeit jedes Materials:

```{code-cell} python
import random
import plotly.express as px

materialien = ["Stahl", "Aluminium", "Titan", "Kupfer"]
ANZAHL_AUFTRAEGE = 120

anzahl_stahl = 0
anzahl_aluminium = 0
anzahl_titan = 0
anzahl_kupfer = 0

for i in range(ANZAHL_AUFTRAEGE):
    material = random.choice(materialien)
    if material == "Stahl":
        anzahl_stahl = anzahl_stahl + 1
    if material == "Aluminium":
        anzahl_aluminium = anzahl_aluminium + 1
    if material == "Titan":
        anzahl_titan = anzahl_titan + 1
    if material == "Kupfer":
        anzahl_kupfer = anzahl_kupfer + 1

fig = px.bar(x=materialien,
             y=[anzahl_stahl, anzahl_aluminium, anzahl_titan, anzahl_kupfer],
             labels={"x": "Material", "y": "Anzahl Aufträge"},
             title=f"Materialverteilung: {ANZAHL_AUFTRAEGE} simulierte Aufträge")
fig.show()
```

```{admonition} Mini-Übung
:class: tip
In einem Lager sind nicht alle Materialien gleich häufig vorrätig. Angenommen,
Stahl ist dreimal so häufig wie die anderen Materialien. Passen Sie die Liste
`materialien` so an, dass Stahl dreimal häufiger ausgewählt wird als jedes der
anderen drei Materialien. Führen Sie die Simulation erneut durch und überprüfen
Sie das Ergebnis im Diagramm.
```

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import random
import plotly.express as px

# Stahl dreimal in der Liste -> dreimal so haeufig ausgewaehlt
materialien_gewichtet = ["Stahl", "Stahl", "Stahl",
                         "Aluminium", "Titan", "Kupfer"]
ANZAHL_AUFTRAEGE = 120

anzahl_stahl = 0
anzahl_aluminium = 0
anzahl_titan = 0
anzahl_kupfer = 0

for i in range(ANZAHL_AUFTRAEGE):
    material = random.choice(materialien_gewichtet)
    if material == "Stahl":
        anzahl_stahl = anzahl_stahl + 1
    if material == "Aluminium":
        anzahl_aluminium = anzahl_aluminium + 1
    if material == "Titan":
        anzahl_titan = anzahl_titan + 1
    if material == "Kupfer":
        anzahl_kupfer = anzahl_kupfer + 1

fig = px.bar(x=["Stahl", "Aluminium", "Titan", "Kupfer"],
             y=[anzahl_stahl, anzahl_aluminium, anzahl_titan, anzahl_kupfer],
             labels={"x": "Material", "y": "Anzahl Aufträge"},
             title=f"Materialverteilung: {ANZAHL_AUFTRAEGE} simulierte Aufträge")
fig.show()
```

Da "Stahl" dreimal in der Liste steht, wird es von `random.choice()` mit einer
Wahrscheinlichkeit von 3/6 = 50 % ausgewählt, während jedes andere Material
nur mit 1/6 ausgewählt wird.
````

```{dropdown} Video "random-Modul in Python" von Programmieren Starten
<iframe width="560" height="315" src="https://www.youtube.com/embed/KzqSDvzOFNA"
title="YouTube video player" frameborder="0" allow="accelerometer; autoplay;
clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
allowfullscreen></iframe>
```

## Zusammenfassung und Ausblick

In diesem Kapitel haben wir das `random`-Modul kennengelernt. Mit
`random.uniform()` haben wir kontinuierliche Streuung simuliert und dabei
direkt an das Qualitätsprüf-Beispiel aus Kapitel 5.8 angeknüpft. Wir haben
gesehen, dass mit steigender Simulationsanzahl das Ergebnis stabiler wird, was
das Grundprinzip der Monte-Carlo-Simulation ist. Mit `random.randint()` haben
wir diskrete Zufallsprozesse wie den Würfelwurf nachgebildet, und mit
`random.choice()` zufällige Auswahlen aus Listen getroffen. In den Übungen
vertiefen wir diese Konzepte mit weiteren Anwendungen aus dem Maschinenbau.
