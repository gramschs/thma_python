---
kernelspec:
  name: python3
  display_name: 'Python 3'
---

# Übungen

````{admonition} Übung 6.1 (✩)
:class: tip
Gegeben ist folgende Liste mit den Wochentagen:

```python
wochentage = ["Montag", "Dienstag", "Mittwoch", "Donnerstag", "Freitag", "Samstag", "Sonntag"]
```

1. Sagen Sie vorher, was die folgenden Ausdrücke ausgeben. Notieren Sie Ihre
   Antwort, bevor Sie den Code ausführen.
   - `wochentage[-1]`
   - `wochentage[-2]`
   - `wochentage[-7]`
   - `wochentage[-4]`
2. Führen Sie den Code aus und überprüfen Sie Ihre Vorhersage.
3. Erklären Sie: Warum liefert `wochentage[-7]` dasselbe Ergebnis wie
   `wochentage[0]`?
4. Was passiert bei `wochentage[-8]`?
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
1. Vorhersage:
   - `wochentage[-1]` gibt `"Sonntag"` aus (letztes Element)
   - `wochentage[-2]` gibt `"Samstag"` aus (vorletztes Element)
   - `wochentage[-7]` gibt `"Montag"` aus (siebtes Element von hinten)
   - `wochentage[-4]` gibt `"Donnerstag"` aus (viertes Element von hinten)

2. Code zur Überprüfung:
```python
wochentage = ["Montag", "Dienstag", "Mittwoch", "Donnerstag", "Freitag", "Samstag", "Sonntag"]

print(wochentage[-1])   # Sonntag
print(wochentage[-2])   # Samstag
print(wochentage[-7])   # Montag
print(wochentage[-4])   # Donnerstag
print(wochentage[-8])   # IndexError
```
3. Erklärung: Die Liste hat 7 Elemente. Python berechnet den positiven Index aus
   dem negativen Index, indem es zum negativen Index die Länge der Liste
   addiert, also `-7 + 7 = 0`. Daher ist `wochentage[-7]` identisch mit
   `wochentage[0]`. Allgemein gilt: Für eine Liste der Länge `n` entspricht
   Index `-n` dem Index `0`. Der Index -8 ist nicht möglich, da die Liste nur 7
   Elemente hat.
````

````{admonition} Übung 6.2 (✩)
:class: tip
An einem Hydrauliksystem werden fortlaufend Druckwerte erfasst und in einer
Liste gespeichert:

```python
druckwerte_bar = [7.2, 8.5, 9.1, 10.3, 11.8, 12.4, 11.9, 10.7]
```

Der maximale Betriebsdruck beträgt 12.0 bar.

1. Geben Sie den zuletzt gemessenen Druckwert aus.
2. Geben Sie den vorletzt gemessenen Druckwert aus.
3. Prüfen Sie, ob der aktuellste Messwert den Maximaldruck überschreitet, und
   geben Sie in diesem Fall `"Warnung: Maximaldruck überschritten!"` aus.
4. Bestimmen Sie mit `len()` die Anzahl der bisherigen Messungen und geben Sie
   aus: `"Anzahl Messungen: {ANZAHL}"`.

Strukturieren Sie Ihren Code mit EVA-Kommentaren.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
# Eingabe
druckwerte_bar = [7.2, 8.5, 9.1, 10.3, 11.8, 12.4, 11.9, 10.7]
MAX_DRUCK_BAR = 12.0

# Verarbeitung und Ausgabe
# 1. Letzter Messwert
print(druckwerte_bar[-1])    # 10.7

# 2. Vorletzter Messwert
print(druckwerte_bar[-2])    # 11.9

# 3. Warnung bei Überschreitung
if druckwerte_bar[-1] > MAX_DRUCK_BAR:
    print("Warnung: Maximaldruck überschritten!")

# 4. Anzahl der Messungen
anzahl = len(druckwerte_bar)
print(f'Anzahl Messungen: {anzahl}')
```

Ausgabe:
```
10.7
11.9
Anzahl Messungen: 8
```

Die Warnung wird nicht ausgegeben, da der letzte Messwert 10.7 bar unterhalb
des Maximaldrucks von 12.0 bar liegt. Der negative Index `-1` ist hier
besonders praktisch: Egal wie viele Messungen noch hinzukommen, er zeigt
immer auf den aktuellsten Wert.
````

````{admonition} Übung 6.3 (✩)
:class: tip
Sie möchten eine formatierte Ausgabe für eine Kontaktliste erstellen. Gegeben
sind folgende Variablen:

```python
name = "Marie Curie"
alter = 35
groesse_m = 1.642
stadt = "Paris"
```

1. Geben Sie mit einem f-String folgenden Satz aus:
   `"Name: Marie Curie, Alter: 35 Jahre, Größe: 1.642 m, Wohnort: Paris"`
2. Geben Sie die Größe auf 2 Nachkommastellen gerundet aus:
   `"Größe: 1.64 m"`
3. Geben Sie das Alter in einem Feld der Breite 5 aus, sodass die Zahl
   rechtsbündig steht:
   `"Alter: [   35] Jahre"` (die eckigen Klammern zeigen das Feld an und
   sollen nicht ausgegeben werden)
4. Erzeugen Sie folgenden Ausgabesatz mit f-String:
   `"Marie Curie ist 35 Jahre alt und 1.64 m groß."`
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
name = "Marie Curie"
alter = 35
groesse_m = 1.642
stadt = "Paris"

# 1. Vollständiger Kontaktsatz
print(f"Name: {name}, Alter: {alter} Jahre, Größe: {groesse_m} m, Wohnort: {stadt}")

# 2. Größe auf 2 Nachkommastellen
print(f"Größe: {groesse_m:.2f} m")

# 3. Alter rechtsbündig in Feld der Breite 5
print(f"Alter: {alter:5d} Jahre")

# 4. Kombination
print(f"{name} ist {alter} Jahre alt und {groesse_m:.2f} m groß.")
```

Ausgabe:
```
Name: Marie Curie, Alter: 35 Jahre, Größe: 1.642 m, Wohnort: Paris
Größe: 1.64 m
Alter:    35 Jahre
Marie Curie ist 35 Jahre alt und 1.64 m groß.
```

Der Formatierungsausdruck `:.2f` rundet auf 2 Nachkommastellen. Der Ausdruck
`:5d` gibt die Ganzzahl in einem Feld der Breite 5 aus und füllt es links
mit Leerzeichen auf.
````

````{admonition} Übung 6.4 (✩✩)
:class: tip
In Kapitel 5.1 haben wir eine Tabelle mit Bremswegen für verschiedene
Geschwindigkeiten berechnet und ausgegeben:

```python
for v in range(30, 131, 10):
    bremsweg = v**2 / 100
    print("v =", v, "km/h,  Bremsweg =", bremsweg, "m")
```

Die Ausgabe enthält viele Nachkommastellen und ist schlecht ausgerichtet.
Darüber hinaus soll jetzt auch der Reaktionsweg

$$s_R = \frac{v}{3.6}$$

und der gesamte Anhalteweg

$$s_{gesamt} = s_R + s_B$$

mit ausgegeben werden.

1. Erweitern Sie den Code so, dass Reaktionsweg und Anhalteweg berechnet
   werden.
2. Formatieren Sie die Ausgabe mit f-Strings so, wie in diesem Beispiel.
```
v =  30 km/h,  Bremsweg =   9.0 m,  Reaktionsweg =  8.3 m,  Anhalteweg =  17.3 m
v =  40 km/h,  Bremsweg =  16.0 m,  Reaktionsweg = 11.1 m,  Anhalteweg =  27.1 m
 ...
v = 130 km/h,  Bremsweg = 169.0 m,  Reaktionsweg = 36.1 m,  Anhalteweg = 205.1 m
```
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
# Verarbeitung und Ausgabe
for v in range(30, 131, 10):
    bremsweg = v**2 / 100
    reaktionsweg = v / 3.6
    anhalteweg = bremsweg + reaktionsweg
    print(f"v = {v:3d} km/h,  Bremsweg = {bremsweg:5.1f} m,  Reaktionsweg = {reaktionsweg:4.1f} m,  Anhalteweg = {anhalteweg:5.1f} m")
```

Ausgabe:
```
v =  30 km/h,  Bremsweg =   9.0 m,  Reaktionsweg =  8.3 m,  Anhalteweg =  17.3 m
v =  40 km/h,  Bremsweg =  16.0 m,  Reaktionsweg = 11.1 m,  Anhalteweg =  27.1 m
v =  50 km/h,  Bremsweg =  25.0 m,  Reaktionsweg = 13.9 m,  Anhalteweg =  38.9 m
v =  60 km/h,  Bremsweg =  36.0 m,  Reaktionsweg = 16.7 m,  Anhalteweg =  52.7 m
v =  70 km/h,  Bremsweg =  49.0 m,  Reaktionsweg = 19.4 m,  Anhalteweg =  68.4 m
v =  80 km/h,  Bremsweg =  64.0 m,  Reaktionsweg = 22.2 m,  Anhalteweg =  86.2 m
v =  90 km/h,  Bremsweg =  81.0 m,  Reaktionsweg = 25.0 m,  Anhalteweg = 106.0 m
v = 100 km/h,  Bremsweg = 100.0 m,  Reaktionsweg = 27.8 m,  Anhalteweg = 127.8 m
v = 110 km/h,  Bremsweg = 121.0 m,  Reaktionsweg = 30.6 m,  Anhalteweg = 151.6 m
v = 120 km/h,  Bremsweg = 144.0 m,  Reaktionsweg = 33.3 m,  Anhalteweg = 177.3 m
v = 130 km/h,  Bremsweg = 169.0 m,  Reaktionsweg = 36.1 m,  Anhalteweg = 205.1 m
```

Hinweis: Alternativ dürfen wir den f-String auch über zwei Zeilen schreiben:
```python
    print(f"v = {v:3d} km/h,  Bremsweg = {bremsweg:5.1f} m,  "
          f"Reaktionsweg = {reaktionsweg:4.1f} m,  Anhalteweg = {anhalteweg:5.1f} m")
```
Ein f-String darf über mehrere Zeilen verteilt werden, indem man ihn
mit `"` beendet und direkt einen neuen f-String beginnt. Python verbindet
beide automatisch zu einer einzigen Ausgabe.
````

````{admonition} Übung 6.5 (✩✩)
:class: tip
Datumsangaben werden in Programmen häufig als String im Format `"YYYY-MM-DD"`
gespeichert, also zum Beispiel `"2024-03-15"` für den 15. März 2024.

```python
datum = "2024-03-15"
```

1. Geben Sie das erste Zeichen des Strings aus. Was stellt dieses Zeichen dar?
2. Geben Sie das letzte und das vorletzte Zeichen aus.
   Was stellen diese beiden Zeichen zusammen dar?
3. Bestimmen Sie die Länge des Strings mit `len()`.
4. Prüfen Sie, ob das Trennzeichen an Position 4
   (Index 4) ein `"-"` ist, und geben Sie in diesem Fall
   `"Gültiges Datumsformat erkannt."` aus.
5. Prüfen Sie, ob das Jahr in der Vergangenheit liegt.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
datum = "2024-03-15"

# 1. Erstes Zeichen
print(datum[0])       # 2  (erste Ziffer der Jahreszahl)

# 2. Letztes und vorletztes Zeichen
print(datum[-1])      # 5  (Einerstelle des Tages)
print(datum[-2])      # 1  (Zehnerstelle des Tages)

# 3. Länge
print(len(datum))     # 10

# 4. Trennzeichen prüfen
if datum[4] == "-":
    print("Gültiges Datumsformat erkannt.")

# 5. Test auf Vergangenheit
jahr = int(datum[0] + datum[1] + datum[2] + datum[3])
if jahr < 2026:
   print(f'{jahr} liegt in der Vergangenheit.')
```

Ausgabe:
```
2
5
1
10
Gültiges Datumsformat erkannt.
2024 liegt in der Vergangenheit.
```
````

````{admonition} Übung 6.6 (✩✩)
:class: tip
Auf einem Jahrmarkt gibt es ein Glücksrad, das *gleichmäßig* in Felder zwischen
0 und 10 unterteilt ist. Landet die Nadel im Bereich von 7.0 bis 10.0, gewinnt
man einen Preis.

Simulieren Sie 200 Drehungen des Glücksrads.

1. Zählen Sie, wie viele der 200 Drehungen in der Gewinnzone landen.
2. Berechnen Sie die Gewinnquote in Prozent.
3. Geben Sie die Ergebnisse aus, z.B. folgendermaßen
   - `"Gewinnzone:    58 von 200 Drehungen"`
   - `"Gewinnquote:   29.0 %"`
4. Visualisieren Sie die 200 Zufallswerte als Histogramm.
   Verwenden Sie als Titel `"Glücksrad: 200 Drehungen"`.

Was erwarten Sie theoretisch für die Gewinnquote? Stimmt Ihr simuliertes
Ergebnis ungefähr damit überein?

Strukturieren Sie Ihren Code mit EVA-Kommentaren.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import numpy as np
import plotly.express as px

# Eingabe
ANZAHL_DREHUNGEN = 200
GEWINNGRENZE_UNTEN = 7.0

# Verarbeitung
anzahl_gewinne = 0
werte = []

for i in range(ANZAHL_DREHUNGEN):
    wert = np.random.uniform(0, 10)
    werte.append(wert)
    if wert >= GEWINNGRENZE_UNTEN:
        anzahl_gewinne = anzahl_gewinne + 1

gewinnquote = anzahl_gewinne / ANZAHL_DREHUNGEN * 100

# Ausgabe
print(f"Gewinnzone:   {anzahl_gewinne} von {ANZAHL_DREHUNGEN} Drehungen")
print(f"Gewinnquote:  {gewinnquote:.1f} %")

fig = px.histogram(x=werte,
                   labels={"x": "Ergebnis"},
                   title="Glücksrad: 200 Drehungen")
fig.show()
```

Theoretische Gewinnquote: Die Gewinnzone umfasst den Bereich von 7.0 bis 10.0,
also 3 von 10 möglichen Einheiten. Die theoretische Gewinnquote beträgt daher
3/10 = 30 %. Das simulierte Ergebnis sollte ungefähr bei 30 % liegen, aber
aufgrund der Zufälligkeit von Durchlauf zu Durchlauf leicht schwanken. Das
Histogramm zeigt annähernd gleich hohe Balken über den gesamten Bereich, was
die Gleichverteilung bestätigt.
````

````{admonition} Übung 6.7 (✩✩)
:class: tip
In einer Fabrik werden Stahlbolzen auf zwei verschiedenen Maschinen gefertigt.
Beide Maschinen sollen denselben Solldurchmesser von 20.0 mm erreichen, aber
sie unterscheiden sich in ihrer Präzision:

* Maschine A: Standardabweichung 0.1 mm (neuere, präzisere Maschine)
* Maschine B: Standardabweichung 0.4 mm (ältere, weniger präzise Maschine)

1. Simulieren Sie mit je einer for-Schleife 500 gefertigte Bolzen pro Maschine.
2. Visualisieren Sie die Durchmesserverteilung beider Maschinen als je ein
   Histogramm.
3. Beschreiben Sie in einer Markdown-Zelle, was Sie in den beiden
   Histogrammen beobachten.

Strukturieren Sie Ihren Code mit EVA-Kommentaren.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import numpy as np
import plotly.express as px

# Eingabe
SOLL_MM = 20.0
SIGMA_A_MM = 0.1   # Maschine A: präzise
SIGMA_B_MM = 0.4   # Maschine B: weniger präzise
ANZAHL_BOLZEN = 500

# Verarbeitung: Simulation beider Maschinen
werte_a = []
werte_b = []

for i in range(ANZAHL_BOLZEN):
    werte_a.append(np.random.normal(loc=SOLL_MM, scale=SIGMA_A_MM))
    werte_b.append(np.random.normal(loc=SOLL_MM, scale=SIGMA_B_MM))

# Ausgabe: Histogramme
fig_a = px.histogram(x=werte_a,
                     labels={"x": "Durchmesser in mm"},
                     title="Maschine A (σ = 0.1 mm): 500 simulierte Bolzen")
fig_a.show()

fig_b = px.histogram(x=werte_b,
                     labels={"x": "Durchmesser in mm"},
                     title="Maschine B (σ = 0.4 mm): 500 simulierte Bolzen")
fig_b.show()
```
Beobachtung: Das Histogramm von Maschine A zeigt eine sehr schmale, hohe
Glockenform. Fast alle Werte liegen sehr nahe am Sollwert 20.0 mm.Das Histogramm
von Maschine B ist deutlich breiter und flacher. Die Werte streuen stark um den
Sollwert, was auf viel Ausschuss hindeutet. Beide Histogramme sind um denselben
Mittelwert 20.0 mm zentriert.
````

````{admonition} Übung 6.8 (✩✩✩)
:class: tip
In der Qualitätssicherung ist die Ausschussquote eine wichtige Kenngröße. Sie
hängt direkt davon ab, wie präzise ein Fertigungsprozess ist.

Eine Welle soll einen Durchmesser von 30.0 mm haben, mit einer zulässigen
Toleranz von ±0.5 mm. Drei verschiedene Fertigungsprozesse werden verglichen,
die alle denselben Mittelwert von 30.0 mm liefern, aber unterschiedlich streuen:

* Prozess 1: Standardabweichung 0.15 mm
* Prozess 2: Standardabweichung 0.25 mm
* Prozess 3: Standardabweichung 0.50 mm

Simulieren Sie für jeden Prozess die Fertigung von 1000 Wellen und berechnen
Sie die Ausschussquote. Geben Sie die Ergebnisse als formatierte Tabelle aus:

```
Prozess | Standardabw. | Ausschussquote
--------|--------------|---------------
      1 |     0.15 mm  |          0.1 %
      2 |     0.25 mm  |          4.6 %
      3 |     0.50 mm  |         31.7 %
```

Definieren Sie Sollwert, Toleranz und Anzahl der Wellen als Konstanten.
Strukturieren Sie Ihren Code mit EVA-Kommentaren.

Hinweis: Schreiben Sie drei separate for-Schleifen, eine für jeden Prozess.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import numpy as np

# Eingabe
SOLL_MM = 30.0
TOLERANZ_MM = 0.5
GRENZE_UNTEN_MM = SOLL_MM - TOLERANZ_MM   # 29.5 mm
GRENZE_OBEN_MM = SOLL_MM + TOLERANZ_MM    # 30.5 mm
ANZAHL_WELLEN = 1000

sigma_1 = 0.15
sigma_2 = 0.25
sigma_3 = 0.50

# Verarbeitung: Prozess 1
anzahl_niO_1 = 0
for i in range(ANZAHL_WELLEN):
    d = np.random.normal(loc=SOLL_MM, scale=sigma_1)
    ist_fehlerhaft = False
    if d < GRENZE_UNTEN_MM:
        ist_fehlerhaft = True
    if d > GRENZE_OBEN_MM:
        ist_fehlerhaft = True
    if ist_fehlerhaft == True:
        anzahl_niO_1 = anzahl_niO_1 + 1

# Verarbeitung: Prozess 2
anzahl_niO_2 = 0
for i in range(ANZAHL_WELLEN):
    d = np.random.normal(loc=SOLL_MM, scale=sigma_2)
    ist_fehlerhaft = False
    if d < GRENZE_UNTEN_MM:
        ist_fehlerhaft = True
    if d > GRENZE_OBEN_MM:
        ist_fehlerhaft = True
    if ist_fehlerhaft == True:
        anzahl_niO_2 = anzahl_niO_2 + 1

# Verarbeitung: Prozess 3
anzahl_niO_3 = 0
for i in range(ANZAHL_WELLEN):
    d = np.random.normal(loc=SOLL_MM, scale=sigma_3)
    ist_fehlerhaft = False
    if d < GRENZE_UNTEN_MM:
        ist_fehlerhaft = True
    if d > GRENZE_OBEN_MM:
        ist_fehlerhaft = True
    if ist_fehlerhaft == True:
        anzahl_niO_3 = anzahl_niO_3 + 1

# Ausschussquoten berechnen
quote_1 = anzahl_niO_1 / ANZAHL_WELLEN * 100
quote_2 = anzahl_niO_2 / ANZAHL_WELLEN * 100
quote_3 = anzahl_niO_3 / ANZAHL_WELLEN * 100

# Ausgabe als formatierte Tabelle
print("Prozess | Standardabw. | Ausschussquote")
print("--------|--------------|---------------")
print(f"      1 |     {sigma_1:.2f} mm  |      {quote_1:6.1f} %")
print(f"      2 |     {sigma_2:.2f} mm  |      {quote_2:6.1f} %")
print(f"      3 |     {sigma_3:.2f} mm  |      {quote_3:6.1f} %")
```

Beispielhafte Ausgabe (Werte variieren durch Zufallszahlen):
```
Prozess | Standardabw. | Ausschussquote
--------|--------------|---------------
      1 |     0.15 mm  |         0.1 %
      2 |     0.25 mm  |         4.3 %
      3 |     0.50 mm  |        32.1 %
```

Erklärung: Die Toleranz beträgt ±0.5 mm. Für Prozess 1 entspricht das ±3.3σ,
weshalb nur sehr wenige Wellen außerhalb der Toleranz liegen. Für Prozess 3
entspricht die Toleranz genau ±1σ: Statistisch liegen dann ca. 31.7 % aller
Werte außerhalb von ±1σ. Da wir mit Zufallszahlen arbeiten, schwanken die
Ergebnisse von Ausführung zu Ausführung leicht um diese theoretischen Werte.
````

````{admonition} Übung 6.9 (✩✩✩) Mini-Projekt
:class: tip
An einer Produktionsanlage wird die Temperatur des Kühlwassers kontinuierlich
überwacht. In der letzten Stunde wurden folgende Messwerte in °C aufgezeichnet:

```python
temperaturen_C = [18.2, 18.7, 19.1, 19.5, 20.3, 20.8, 21.4, 22.1, 22.6, 23.0,
                  23.5, 23.9]
```

Der kritische Grenzwert liegt bei 25.0 °C. Wird dieser überschritten, muss die
Anlage abgekühlt werden.

**Teil 1: Auswertung der Messdaten**

1. Geben Sie den aktuellsten und den ältesten Messwert aus.
2. Berechnen Sie den Mittelwert der bisherigen Messungen mit einer for-Schleife
   (ohne `sum()` oder `mean()`).
3. Geben Sie mit einem f-String aus:
   `"Aktuellster Wert: 23.9 °C  |  Ältester Wert: 18.2 °C  |  Mittelwert: 21.1 °C"`

**Teil 2: Simulation des weiteren Temperaturverlaufs**

Die Temperatur steigt weiter. Simulieren Sie die nächsten 50 Messungen als
normalverteilte Zufallszahlen mit dem Mittelwert aus Teil 1 und einer
Standardabweichung von 1.5 °C.

4. Zählen Sie, wie viele der 50 simulierten Messungen den Grenzwert von 25.0 °C
   überschreiten.
5. Berechnen Sie den Anteil kritischer Messungen in Prozent.
6. Geben Sie aus:
   `"Simulierte Messungen:   50"`,
   `"Kritische Messungen:     8"`,
   `"Anteil kritisch:        16.0 %"`

**Teil 3: Visualisierung**

7. Visualisieren Sie die 50 simulierten Temperaturwerte als Histogramm mit
   dem Titel `"Simulierter Temperaturverlauf: nächste 50 Messungen"`.

Definieren Sie den Grenzwert als Konstante. Strukturieren Sie Ihren Code mit
EVA-Kommentaren.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import numpy as np
import plotly.express as px

# Eingabe
temperaturen_C = [18.2, 18.7, 19.1, 19.5, 20.3, 20.8, 21.4, 22.1, 22.6, 23.0,
                  23.5, 23.9]
GRENZWERT_C = 25.0
ANZAHL_SIMULATIONEN = 50
SIGMA_C = 1.5

# --- Teil 1: Auswertung der Messdaten ---

# 1. Aktuellster und ältester Messwert
aktuellster = temperaturen_C[-1]
aeltester = temperaturen_C[0]

# 2. Mittelwert berechnen
summe = 0
anzahl = 0
for temp in temperaturen_C:
    summe = summe + temp
    anzahl = anzahl + 1
mittelwert = summe / anzahl

# 3. Formatierte Ausgabe
print(f"Aktuellster Wert: {aktuellster:.1f} °C  |  "
      f"Ältester Wert: {aeltester:.1f} °C  |  "
      f"Mittelwert: {mittelwert:.1f} °C")

# --- Teil 2: Simulation ---

# 4. Simulierte Messungen erzeugen und kritische zählen
simulierte_werte = []
anzahl_kritisch = 0

for i in range(ANZAHL_SIMULATIONEN):
    wert = np.random.normal(loc=mittelwert, scale=SIGMA_C)
    simulierte_werte.append(wert)
    if wert > GRENZWERT_C:
        anzahl_kritisch = anzahl_kritisch + 1

# 5. Anteil kritischer Messungen
anteil_kritisch = anzahl_kritisch / ANZAHL_SIMULATIONEN * 100

# 6. Formatierte Ausgabe
print(f"Simulierte Messungen:  {ANZAHL_SIMULATIONEN:3d}")
print(f"Kritische Messungen:   {anzahl_kritisch:3d}")
print(f"Anteil kritisch:       {anteil_kritisch:5.1f} %")

# --- Teil 3: Visualisierung ---

fig = px.histogram(x=simulierte_werte,
                   labels={"x": "Temperatur in °C"},
                   title="Simulierter Temperaturverlauf: nächste 50 Messungen")
fig.show()
```

Beispielhafte Ausgabe (Werte in Teil 2 variieren durch Zufallszahlen):
```
Aktuellster Wert: 23.9 °C  |  Ältester Wert: 18.2 °C  |  Mittelwert: 21.1 °C
Simulierte Messungen:   50
Kritische Messungen:     9
Anteil kritisch:        18.0 %
```

Erklärung: Der Mittelwert der Messdaten beträgt ca. 21.1 °C, der Grenzwert
liegt bei 25.0 °C. Das entspricht einem Abstand von ca. 2.6σ (bei σ = 1.5 °C).
Statistisch liegen ca. 0.5 % aller Werte einer Normalverteilung mehr als 2.6σ
über dem Mittelwert, bei 50 Simulationen also ca. 2 bis 5 kritische Messungen.
Da der Mittelwert der Simulation auf den gemessenen Daten basiert und mit
Zufallszahlen gearbeitet wird, schwanken die Ergebnisse von Ausführung zu
Ausführung.

Dieses Mini-Projekt zeigt einen typischen Arbeitsablauf in der
Prozessüberwachung: Reale Messdaten auswerten, statistische Kenngrößen
berechnen und auf deren Basis den weiteren Verlauf simulieren.
````
