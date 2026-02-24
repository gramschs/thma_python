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
Ingenieurinnen und Ingenieure **Simulationen**. In diesem Kapitel lernen wir
mit `numpy.random` ein mächtiges Werkzeug kennen, das Zufallszahlen für genau
solche Simulationen bereitstellt.

## Lernziele

```{admonition} Lernziele
:class: attention
* [ ] Sie können NumPy mit dem Alias `np` importieren.
* [ ] Sie können mit `np.random.uniform()` gleichverteilte Zufallszahlen
  erzeugen.
* [ ] Sie können mit `np.random.normal()` normalverteilte Zufallszahlen erzeugen
  und kennen die Parameter **Mittelwert** und **Standardabweichung**.
* [ ] Sie können mit `np.random.randint()` ganzzahlige Zufallszahlen erzeugen.
* [ ] Sie können Zufallszahlen mit einer for-Schleife kombinieren, um einfache
  Simulationen durchzuführen.
```

## NumPy: ein erster Blick

NumPy ist das wichtigste Modul für wissenschaftliches Rechnen in Python. Es
stellt unter anderem effiziente Funktionen für mathematische Operationen,
lineare Algebra und Statistik bereit. In einem späteren Kapitel werden wir NumPy
ausführlich kennenlernen. Für dieses Kapitel interessiert uns zunächst nur ein
Teilbereich: `numpy.random`, also die Zufallszahlen-Funktionen von NumPy.

NumPy wird mit dem Standard-Alias `np` importiert:

```{code-cell} python
import numpy as np
```

Danach stehen alle NumPy-Funktionen über `np.` zur Verfügung, also zum Beispiel
`np.random.uniform()` oder `np.random.normal()`.

## Gleichverteilte Zufallszahlen: np.random.uniform()

Die Funktion `np.random.uniform(low, high)` erzeugt eine zufällige
Fließkommazahl, die gleichmäßig zwischen `low` und `high` verteilt ist. Das
bedeutet: Jeder Wert innerhalb dieses Bereichs ist gleich wahrscheinlich.

Als erstes einfaches Modell nehmen wir an, dass die Durchmesser gefertigter
Bolzen gleichmäßig zwischen 24.5 mm und 25.5 mm streuen:

```{code-cell} python
import numpy as np

durchmesser = np.random.uniform(24.5, 25.5)
print(f"Simulierter Durchmesser: {durchmesser:.3f} mm")
```

Jedes Mal, wenn wir diese Zelle ausführen, erhalten wir einen anderen Wert.

```{admonition} Mini-Übung
:class: tip
Führen Sie die obige Code-Zelle fünfmal hintereinander aus. Liegen alle Werte
zwischen 24.5 und 25.5? Was passiert, wenn Sie die Grenzen auf 24.8 und 25.2
einengen?
```

````{admonition} Lösung
:class: tip
:class: dropdown
Alle erzeugten Werte liegen innerhalb der angegebenen Grenzen. Bei engeren
Grenzen (24.8 bis 25.2) streuen die Werte entsprechend weniger, was einem
präziseren Fertigungsprozess entspricht.
````

## Normalverteilte Zufallszahlen: np.random.normal()

Die Gleichverteilung ist zwar einfach zu verstehen, aber in der Realität folgt
die Streuung von Fertigungsmaßen fast immer einer **Normalverteilung** (auch
Gauß-Verteilung genannt). Bei einer Normalverteilung liegen die meisten Werte
nahe am Mittelwert, und je weiter ein Wert vom Mittelwert entfernt ist, desto
seltener tritt er auf. Das kennen wir aus dem Alltag: Die meisten Menschen haben
eine Körpergröße nahe dem Durchschnitt, sehr kleine oder sehr große Menschen
sind selten.

Die Normalverteilung wird durch zwei Parameter beschrieben:

* **Mittelwert** $\mu$ (griechisch: mu; wird "mü" ausgesprochen): Der Wert, um
  den die Messwerte zentriert sind. Bei unserem Bolzen entspricht das dem
  Solldurchmesser 25.0 mm.
* **Standardabweichung** $\sigma$ (griechisch: sigma): Ein Maß dafür, wie breit
  die Streuung ist. Eine kleine Standardabweichung bedeutet einen präzisen
  Prozess, eine große bedeutet viel Streuung.

Die Funktion `np.random.normal(loc, scale)` erzeugt eine normalverteilte
Zufallszahl, wobei `loc` dem Mittelwert und `scale` der Standardabweichung
entspricht:

```{code-cell} python
import numpy as np

# Bolzendurchmesser: Mittelwert 25.0 mm, Standardabweichung 0.15 mm
durchmesser = np.random.normal(loc=25.0, scale=0.15)
print(f"Simulierter Durchmesser: {durchmesser:.3f} mm")
```

```{admonition} Mini-Übung
:class: tip
Welches Modell ist realistischer für einen Fertigungsprozess:
`np.random.uniform(24.5, 25.5)` oder `np.random.normal(loc=25.0, scale=0.15)`?
Begründen Sie Ihre Antwort.
```

````{admonition} Lösung
:class: tip
:class: dropdown
`np.random.normal(loc=25.0, scale=0.15)` ist realistischer. In einem
Fertigungsprozess ist der Solldurchmesser das angestrebte Ziel. Kleine
Abweichungen davon treten häufig auf, große Abweichungen sind selten. Das
entspricht genau der Normalverteilung. Die Gleichverteilung würde hingegen
bedeuten, dass jeder Durchmesser zwischen 24.5 mm und 25.5 mm gleich
wahrscheinlich ist, also ein Bolzen von 24.51 mm genauso häufig vorkommt wie
einer von 25.0 mm. Das ist physikalisch nicht realistisch.
````

## Fertigungsprozess simulieren

Jetzt kombinieren wir `np.random.normal()` mit einer for-Schleife und der
Qualitätsprüfung aus Übung 5.8. Wir simulieren die Fertigung von 500 Bolzen
und prüfen für jeden, ob er innerhalb der Toleranz von 25.0 mm ± 0.3 mm liegt:

```{code-cell} python
import numpy as np
import plotly.express as px

# Toleranzgrenzen aus Sollwert und Toleranz berechnen
SOLL_MM = 25.0
TOLERANZ_MM = 0.3
GRENZE_UNTEN_MM = SOLL_MM - TOLERANZ_MM   # 24.7 mm
GRENZE_OBEN_MM = SOLL_MM + TOLERANZ_MM    # 25.3 mm
ANZAHL_BOLZEN = 500

anzahl_iO = 0
anzahl_niO = 0

for i in range(ANZAHL_BOLZEN):
    # Durchmesser eines Bolzens simulieren: normalverteilt um den Sollwert
    d = np.random.normal(loc=SOLL_MM, scale=0.15)

    # Prüfen, ob der Bolzen innerhalb der Toleranz liegt
    ist_fehlerhaft = False
    if d < GRENZE_UNTEN_MM:
        ist_fehlerhaft = True   # zu klein
    if d > GRENZE_OBEN_MM:
        ist_fehlerhaft = True   # zu groß

    # Zähler je nach Ergebnis erhöhen
    if ist_fehlerhaft == True:
        anzahl_niO = anzahl_niO + 1
    if ist_fehlerhaft == False:
        anzahl_iO = anzahl_iO + 1

# Ausschussquote in Prozent berechnen
ausschussquote = anzahl_niO / ANZAHL_BOLZEN * 100

print(f"iO-Teile:       {anzahl_iO}")
print(f"niO-Teile:      {anzahl_niO}")
print(f"Ausschussquote: {ausschussquote:.1f} %")

# Visualisierung
fig = px.bar(x=["iO-Teile", "niO-Teile"],
             y=[anzahl_iO, anzahl_niO],
             labels={"x": "Klassifizierung", "y": "Anzahl Bolzen"},
             title=f"Qualitätsprüfung: Simulation von {ANZAHL_BOLZEN} Bolzen")
fig.show()
```

Bei einer Standardabweichung von 0.15 mm und einer Toleranz von ±0.3 mm
liegen die Grenzen bei ±2σ (zwei Standardabweichungen). Die Statistik sagt,
dass bei einer Normalverteilung ca. 95.4 % aller Werte innerhalb von ±2σ
liegen. Die Ausschussquote sollte daher bei ca. 4.6 % liegen.

```{admonition} Mini-Übung
:class: tip
Verändern Sie die Standardabweichung auf 0.05 mm (sehr präziser Prozess) und
dann auf 0.3 mm (wenig präziser Prozess). Beobachten Sie, wie sich die
Ausschussquote verändert. Was passiert mit der Ausschussquote, wenn die
Standardabweichung gleich der Toleranz ist?
```

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
Bei `scale=0.05` (Toleranz entspricht 6σ) ist die Ausschussquote nahezu 0 %.
Bei `scale=0.15` (Toleranz entspricht 2σ) liegt die Ausschussquote bei ca. 4.6 %.
Bei `scale=0.3` (Toleranz entspricht 1σ) liegt die Ausschussquote bei ca. 31.7 %,
da statistisch nur ca. 68.3 % aller Werte innerhalb von ±1σ liegen.

Das zeigt: Die Ausschussquote hängt direkt vom Verhältnis zwischen Toleranz und
Standardabweichung ab. In der Qualitätssicherung spricht man vom
**Fähigkeitsindex** $C_p$, der genau dieses Verhältnis beschreibt. Ein
Fertigungsprozess gilt als fähig, wenn $C_p \geq 1.33$, also wenn die Toleranz
mindestens 4σ beträgt. Das werden wir in einem späteren Kapitel genauer
untersuchen.
````

## Ganzzahlige Zufallszahlen: np.random.randint()

Die Funktion `np.random.randint(low, high)` erzeugt eine zufällige ganze Zahl
zwischen `low` (einschließlich) und `high` (ausschließlich). Achtung: Anders
als bei `np.random.uniform()` ist die obere Grenze hier nicht enthalten.

Mit `np.random.randint(1, 7)` simulieren wir den Wurf eines fairen Würfels:

```{code-cell} python
import numpy as np

wurf = np.random.randint(1, 7)
print(f"Gewürfelt: {wurf}")
```

Der Würfelwurf mag auf den ersten Blick wenig mit Maschinenbau zu tun haben.
Er ist jedoch ein einfaches Modell für diskrete Zufallsprozesse, die auch im
Ingenieurwesen auftreten, zum Beispiel die Anzahl von Fehlern pro gefertigtem
Bauteil oder die Anzahl von Maschinenausfällen pro Woche.

Mit einer for-Schleife simulieren wir 600 Würfe und prüfen, ob alle sechs
Augenzahlen ungefähr gleich häufig auftreten:

```{code-cell} python
import numpy as np
import plotly.express as px

ANZAHL_WUERFE = 600

haeufigkeit = [0, 0, 0, 0, 0, 0]

for i in range(ANZAHL_WUERFE):
    wurf = np.random.randint(1, 7)
    haeufigkeit[wurf - 1] = haeufigkeit[wurf - 1] + 1

print("Augenzahl | Häufigkeit | Erwartung")
for augenzahl in range(1, 7):
    h = haeufigkeit[augenzahl - 1]
    print(f"    {augenzahl}     |    {h:3d}     |    {ANZAHL_WUERFE // 6}")

fig = px.bar(x=[1, 2, 3, 4, 5, 6],
             y=haeufigkeit,
             labels={"x": "Augenzahl", "y": "Häufigkeit"},
             title=f"Würfelsimulation: {ANZAHL_WUERFE} Würfe")
fig.show()
```

Beachten Sie `haeufigkeit[wurf - 1]`: Da Python mit Index 0 beginnt, entspricht
Augenzahl 1 dem Index 0 und Augenzahl 6 dem Index 5. Der ganzzahlige
Divisionsoperator `//` liefert den Erwartungswert als ganze Zahl.

```{admonition} Mini-Übung
:class: tip
Erhöhen Sie die Anzahl der Würfe auf 6000 und dann auf 60000. Beobachten Sie,
wie sich die Abweichungen vom Erwartungswert verändern. Was schlussfolgern Sie
daraus für die Verlässlichkeit von Simulationen?
```

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
Bei 600 Würfen schwanken die Häufigkeiten merklich um den Erwartungswert 100.
Bei 6000 Würfen sind die relativen Abweichungen bereits deutlich kleiner.
Bei 60000 Würfen sehen die Balken im Diagramm nahezu gleich hoch aus, obwohl
absolute Abweichungen noch vorhanden sind.

Das ist das **Gesetz der großen Zahlen**: Mit steigender Anzahl nähert sich
die beobachtete Häufigkeit der theoretischen Wahrscheinlichkeit an. Für
Simulationen bedeutet das: Je mehr Durchläufe, desto verlässlicher das
Ergebnis. In der Ingenieurpraxis spricht man von der **Monte-Carlo-Simulation**,
die genau dieses Prinzip nutzt, zum Beispiel bei der Zuverlässigkeitsberechnung
oder der Risikoanalyse von Maschinen und Anlagen.
````

## Zusammenfassung und Ausblick

In diesem Kapitel haben wir NumPy zum ersten Mal kennengelernt und mit
`numpy.random` erste Simulationen durchgeführt. Mit `np.random.uniform()` haben
wir gleichverteilte Streuung modelliert und mit `np.random.normal()` das
realistischere Modell der Normalverteilung eingeführt, das direkt auf den
Fertigungsprozess aus Kapitel 5.8 angewendet wurde. Der Vergleich beider
Modelle hat gezeigt, warum die Wahl des richtigen Verteilungsmodells in der
Simulation wichtig ist. Mit `np.random.randint()` haben wir diskrete
Zufallsprozesse simuliert und dabei das Gesetz der großen Zahlen beobachtet,
das die Grundlage der Monte-Carlo-Simulation bildet. In den Übungen vertiefen
wir diese Konzepte. In einem späteren Kapitel werden wir NumPy vollständig
einführen und seine Möglichkeiten für wissenschaftliches Rechnen ausschöpfen.
