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
* [ ] Sie kennen den Unterschied zwischen **Gleichverteilung** und
  **Normalverteilung** und können erklären, welches Modell für
  Fertigungsstreuung realistischer ist.
* [ ] Sie können NumPy mit dem Alias `np` importieren.
* [ ] Sie können mit `np.random.uniform()` gleichverteilte Zufallszahlen
  erzeugen.
* [ ] Sie können mit `np.random.normal()` normalverteilte Zufallszahlen erzeugen
  und kennen die Parameter **Mittelwert** und **Standardabweichung**.
* [ ] Sie können mit `px.histogram()` die Verteilung von Zufallszahlen
  visualisieren.
```

## Gleichverteilung und Normalverteilung

Bevor wir Zufallszahlen erzeugen, müssen wir uns fragen: Wie sind die Werte
in der Realität verteilt? Zwei Modelle sind besonders wichtig.

Bei der **Gleichverteilung** ist jeder Wert innerhalb eines Bereichs gleich
wahrscheinlich. Beispielsweise ist bei einem sechsseitigen Würfel jede Augenzahl
von 1 bis 6 gleich wahrscheinlich.

Bei der **Normalverteilung** liegen die meisten Werte nahe einem Mittelwert, und
je weiter ein Wert vom Mittelwert entfernt ist, desto seltener tritt er auf. Das
kennen wir aus dem Alltag: Die meisten Menschen haben eine Körpergröße nahe dem
Durchschnitt, sehr kleine oder sehr große Menschen sind selten.

Für einen Fertigungsprozess gilt: Die Maschine versucht, den Solldurchmesser
zu treffen. Kleine Abweichungen passieren ständig, große Abweichungen sind
selten. Das entspricht einer Normalverteilung. Eine Gleichverteilung würde
bedeuten, dass ein Bolzen von 24.51 mm genauso häufig vorkommt wie einer von
25.0 mm, was nicht realistisch ist.

## Zufallszahlen mit NumPy

NumPy ist das wichtigste Modul für wissenschaftliches Rechnen in Python. Es
stellt unter anderem effiziente Funktionen für mathematische Operationen,
lineare Algebra und Statistik bereit. In einem späteren Kapitel werden wir NumPy
ausführlich kennenlernen. Für dieses Kapitel interessiert uns zunächst nur ein
Teilbereich: `numpy.random`, also die Zufallszahlen-Funktionen von NumPy.

NumPy wird mit dem Standard-Alias `np` importiert:

```{code-cell} python
import numpy as np
```

Danach stehen alle NumPy-Funktionen über `np.` zur Verfügung.

Die Funktion `np.random.uniform(low, high)` erzeugt eine **gleichverteilte
Zufallszahl** zwischen `low` und `high`:

```{code-cell} python
durchmesser = np.random.uniform(24.5, 25.5)
print(f"Simulierter Durchmesser: {durchmesser:.3f} mm")
```

Jedes Mal, wenn wir diese Zelle ausführen, erhalten wir einen anderen Wert,
der gleichmäßig zwischen 24.5 mm und 25.5 mm verteilt ist.

Die Funktion `np.random.normal(loc, scale)` erzeugt eine **normalverteilte
Zufallszahl**. Der Parameter `loc` gibt den **Mittelwert** an, also den Wert, um
den die Zufallszahlen zentriert sind. Der Parameter `scale` gibt die
**Standardabweichung** an, also ein Maß dafür, wie breit die Streuung ist. Eine
kleine Standardabweichung bedeutet einen präzisen Prozess, eine große bedeutet
viel Streuung.

```{code-cell} python
# Bolzendurchmesser: Mittelwert 25.0 mm, Standardabweichung 0.15 mm
durchmesser = np.random.normal(loc=25.0, scale=0.15)
print(f"Simulierter Durchmesser: {durchmesser:.3f} mm")
```

```{admonition} Hinweis für Fortgeschrittene
:class: caution
Seit NumPy 1.17 empfiehlt NumPy den neuen Generator-API mit
`rng = np.random.default_rng()`. Wir verwenden hier den klassischen
Aufrufstil, der einsteigerfreundlicher ist und in der Praxis weit
verbreitet bleibt.
```

## Verteilungen sichtbar machen: px.histogram()

Ein einzelner Zufallswert verrät wenig darüber, wie sich viele Werte verteilen.
Mit einem **Histogramm** können wir das sichtbar machen. Ein Histogramm teilt
den Wertebereich in gleich breite Abschnitte (sogenannte Bins) und zählt, wie
viele Werte in jeden Abschnitt fallen. Plotly Express stellt dafür die Funktion
`px.histogram()` bereit, die wir in einem späteren Kapitel ausführlich
kennenlernen werden. Für jetzt genügt es zu wissen, dass wir eine Liste von
Werten übergeben und ein Histogramm erhalten.

Wir erzeugen 1000 gleichverteilte und 1000 normalverteilte Bolzendurchmesser
und visualisieren beide als Histogramm:

```{code-cell} python
import numpy as np
import plotly.express as px

# 1000 gleichverteilte Durchmesser zwischen 24.5 mm und 25.5 mm
werte_gleichverteilt = []
for i in range(1000):
    werte_gleichverteilt.append(np.random.uniform(24.5, 25.5))

# 1000 normalverteilte Durchmesser: Mittelwert 25.0 mm, Standardabweichung 0.15 mm
werte_normalverteilt = []
for i in range(1000):
    werte_normalverteilt.append(np.random.normal(loc=25.0, scale=0.15))

fig_gleich = px.histogram(x=werte_gleichverteilt,
                          labels={"x": "Durchmesser in mm", "y": "Häufigkeit"},
                          title="Gleichverteilung: 1000 simulierte Bolzen")
fig_gleich.show()

fig_normal = px.histogram(x=werte_normalverteilt,
                          labels={"x": "Durchmesser in mm", "y": "Häufigkeit"},
                          title="Normalverteilung: 1000 simulierte Bolzen")
fig_normal.show()
```

Das Histogramm der Gleichverteilung zeigt annähernd gleich hohe Balken über den
gesamten Bereich. Das Histogramm der Normalverteilung zeigt die typische
Glockenform: Werte nahe 25.0 mm treten am häufigsten auf, nach außen hin werden
die Balken immer kleiner.

```{admonition} Mini-Übung
:class: tip
Verändern Sie die Standardabweichung der Normalverteilung auf 0.05 mm und dann
auf 0.5 mm. Beobachten Sie, wie sich die Form des Histogramms verändert. Was
passiert mit der Breite der Glocke?
```

````{admonition} Lösung
:class: tip
:class: dropdown
Bei `scale=0.05` ist die Glocke sehr schmal und hoch: Fast alle Werte liegen
nahe am Mittelwert 25.0 mm, was einem sehr präzisen Fertigungsprozess
entspricht. Bei `scale=0.5` ist die Glocke sehr breit und flach: Die Werte
streuen stark um den Mittelwert. Ein breiteres Histogramm bedeutet also mehr
Fertigungsstreuung und damit eine höhere Ausschussquote.
````

```{admonition} Ausblick
:class: caution
In diesem Kapitel füllen wir Listen mit einer for-Schleife. NumPy bietet
eine kompaktere Alternative: `np.random.normal(loc=25.0, scale=0.15, size=1000)`
erzeugt 1000 Zufallszahlen in einer einzigen Zeile. Diese sogenannte
**Vektorisierung** ist einer der zentralen Vorteile von NumPy und wird im
NumPy-Kapitel ausführlich behandelt.
```

## Zusammenfassung und Ausblick

In diesem Kapitel haben wir NumPy zum ersten Mal kennengelernt und mit
`numpy.random` erste Simulationen durchgeführt. Wir haben den Unterschied
zwischen Gleichverteilung und Normalverteilung kennengelernt und mit
`px.histogram()` sichtbar gemacht, warum die Normalverteilung für
Fertigungsprozesse das realistischere Modell ist. In einem späteren Kapitel
werden wir NumPy vollständig einführen, Histogramme vertiefen und die Simulation
um weitere statistische Kenngrößen ergänzen.
