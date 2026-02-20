---
kernelspec:
  name: python3
  display_name: 'Python 3'
---

# Übungen

````{admonition} Übung 4.1
:class: tip
Gegeben ist folgende Variable:
```python
x = 15
```

Sagen Sie vorher, welches Ergebnis die folgenden Vergleiche liefern (`True` oder
`False`), und notieren Sie Ihre Antwort. Führen Sie anschließend den Code aus
und überprüfen Sie Ihre Vorhersage.

1. `x >= 10`
2. `x != 15`
3. `x > 15`
4. `x < 20`
5. `x == 15`
6. `x <= 15`
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
x = 15

print(x >= 10)  # True,  da 15 größer oder gleich 10 ist
print(x != 15)  # False, da 15 gleich 15 ist, also nicht ungleich
print(x > 15)   # False, da 15 nicht größer als 15 ist
print(x < 20)   # True,  da 15 kleiner als 20 ist
print(x == 15)  # True,  da 15 gleich 15 ist
print(x <= 15)  # True,  da 15 kleiner oder gleich 15 ist
```

Ausgabe:
```
True
False
False
True
True
True
```
````

````{admonition} Übung 4.2
:class: tip
Gegeben sind folgende Variablen:
```python
stadt1 = "Ludwigshafen"
stadt2 = "ludwigshafen"
stadt3 = "Mannheim"
stadt4 = "mannheim"
```

Sagen Sie vorher, welches Ergebnis die folgenden Vergleiche liefern (`True` oder
`False`), und notieren Sie Ihre Antwort. Führen Sie anschließend den Code aus
und überprüfen Sie Ihre Vorhersage.

1. `stadt1 == stadt2`
2. `stadt1 != stadt2`
3. `stadt1 < stadt3`
4. `stadt4 < stadt3`
5. `"hafen" in stadt1`
6. `"mannheim" == stadt3`
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
stadt1 = "Ludwigshafen"
stadt2 = "ludwigshafen"
stadt3 = "Mannheim"
stadt4 = "mannheim"

print(stadt1 == stadt2)     # False, da Python Groß-/Kleinschreibung unterscheidet
print(stadt1 != stadt2)     # True,  da "Ludwigshafen" und "ludwigshafen" nicht identisch sind
print(stadt1 < stadt3)      # True,  da "L" vor "M" kommt
print(stadt4 < stadt3)      # False, da Kleinbuchstaben als größer gelten als Großbuchstaben
print("hafen" in stadt1)    # True,  da "hafen" in "Ludwigshafen" enthalten ist
print("mannheim" == stadt3) # False, da Groß-/Kleinschreibung unterschiedlich ist
```

Ausgabe:
```
False
True
True
False
True
False
```
````

```{admonition} Übung 4.3
:class: tip
In einer Lehrveranstaltung gilt: Wer mindestens 50 Punkte erreicht, hat die
Prüfung bestanden.

Schreiben Sie ein Skript, das nach der erreichten Punktzahl fragt. Wenn die
Punktzahl mindestens 50 beträgt, soll ausgegeben werden: "Bestanden! Herzlichen
Glückwunsch."

Strukturieren Sie Ihren Code mit EVA-Kommentaren.
```

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
# Eingabe
punkte = float(input('Wie viele Punkte haben Sie erreicht? '))

# Verarbeitung und Ausgabe
if punkte >= 50:
    print('Bestanden! Herzlichen Glückwunsch.')
```
````

```{admonition} Übung 4.4
:class: tip
An einem Prüfstand wird der Luftdruck in einem Behälter gemessen. Der maximale
Betriebsdruck beträgt 12.0 bar. Wird dieser Wert überschritten, muss ein
Sicherheitsventil geöffnet werden.

Schreiben Sie ein Skript, das nach dem gemessenen Druck in bar fragt. Wenn der
Druck den maximalen Betriebsdruck überschreitet, soll ausgegeben werden:
"Warnung: Maximaldruck überschritten. Sicherheitsventil öffnen."

Strukturieren Sie Ihren Code mit EVA-Kommentaren.
```

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
# Eingabe
druck_bar = float(input('Welchen Druck hat der Behälter aktuell (in bar)? '))

# Verarbeitung und Ausgabe
if druck_bar > 12.0:
    print('Warnung: Maximaldruck überschritten. Sicherheitsventil öffnen.')
```
````

```{admonition} Übung 4.5
:class: tip
An einem internationalen Flughafen werden Passagiere in ihrer Landessprache
begrüßt. Schreiben Sie ein Skript, das nach dem Kürzel der gewünschten Sprache
fragt. Geben Sie dann die passende Begrüßung aus:

* Wenn `"DE"` eingegeben wird: "Willkommen!"
* Wenn `"EN"` eingegeben wird: "Welcome!"
* Wenn `"FR"` eingegeben wird: "Bienvenue!"

Strukturieren Sie Ihren Code mit EVA-Kommentaren.
```

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
# Eingabe
sprache = input('Bitte geben Sie das Sprachkürzel ein (DE/EN/FR): ')

# Verarbeitung und Ausgabe
if sprache == 'DE':
    print('Willkommen!')
if sprache == 'EN':
    print('Welcome!')
if sprache == 'FR':
    print('Bienvenue!')
```
````

```{admonition} Übung 4.6
:class: tip
Bei der Überwachung einer Produktionsanlage wird die Betriebstemperatur in drei
Bereiche eingeteilt:

* Unter 60 °C: Normalbetrieb
* Ab 60 °C: erhöhte Betriebstemperatur
* Ab 80 °C: kritischer Bereich

Schreiben Sie ein Skript, das nach der aktuellen Betriebstemperatur fragt und
für jeden zutreffenden Bereich eine passende Meldung ausgibt. Strukturieren Sie
Ihren Code mit EVA-Kommentaren.

Testen Sie Ihr Skript anschließend mit folgenden Temperaturen und notieren Sie
jeweils, welche Meldungen ausgegeben werden:

* 45 °C
* 70 °C
* 95 °C

Was beobachten Sie bei 95 °C? Warum werden bei dieser Temperatur zwei Meldungen
ausgegeben?
```

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
# Eingabe
temperatur_C = float(input('Wie hoch ist die aktuelle Betriebstemperatur (in °C)? '))

# Verarbeitung und Ausgabe
if temperatur_C < 60:
    print('Normalbetrieb.')
if temperatur_C >= 60:
    print('erhöhte Betriebstemperatur.')
if temperatur_C >= 80:
    print('kritischer Bereich.')
```

Testergebnisse:

* 45 °C → `Normalbetrieb.`
* 70 °C → `erhöhte Betriebstemperatur.`
* 95 °C → `erhöhte Betriebstemperatur.` und `kritischer Bereich.`

Erklärung: Bei 95 °C sind zwei Bedingungen gleichzeitig wahr, sowohl
`temperatur_C >= 60` als auch `temperatur_C >= 80`. Da alle drei `if`-Blöcke
**unabhängig voneinander** ausgewertet werden, gibt Python beide Meldungen aus.
Das ist kein Fehler, sondern das erwartete Verhalten bei mehreren unabhängigen
`if`-Blöcken.

In einem späteren Kapitel werden wir `if-elif-else` kennenlernen. Damit lässt
sich sicherstellen, dass immer genau eine Meldung ausgegeben wird. Sobald eine
Bedingung erfüllt ist, werden die übrigen nicht mehr geprüft.
````

````{admonition} Übung 4.7
:class: tip
Gegeben ist folgende Liste mit den aktuellen Tabellenplätzen 1 bis 5 
der 1. Fußball-Bundesliga:
```python
tabelle = ["Bayern München", "Borussia Dortmund", "TSG Hoffenheim", "VfB Stuttgart", "RB Leipzig"]
```

Schreiben Sie ein Skript, das den Benutzer oder die Benutzerin fragt: "Welcher
Verein steht aktuell auf Platz 3?" Wenn die Antwort korrekt ist, soll ausgegeben
werden: "Richtig!"

Geben Sie anschließend aus, welcher Verein tatsächlich auf dem eingegebenen
Tabellenplatz steht.

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
tabelle = ["Bayern München", "Borussia Dortmund", "TSG Hoffenheim", "VfB Stuttgart", "RB Leipzig"]
antwort = input('Welcher Verein steht aktuell auf Platz 3? ')

# Verarbeitung und Ausgabe
if antwort == tabelle[2]:
    print('Richtig!')
print('Auf Platz 3 steht:', tabelle[2])
```
Für den Zugriff auf den 3. Platz in der Tabelle benutzen wir Index 2.
````

````{admonition} Übung 4.8
:class: tip
:class: tip
Gegeben sind folgende Messwerte der Bremsscheibentemperatur:
```python
zeit_s = [0, 0.5, 1.0, 1.5, 2.0, 2.5, 3.0]
temperatur_celsius = [80, 145, 210, 265, 305, 335, 350]
```

Berechnen Sie den Durchschnitt der Temperaturwerte, indem Sie die einzelnen
Listenelemente über ihren Index addieren und durch die Anzahl der Messungen
teilen.

Erstellen Sie anschließend ein Liniendiagramm mit Titel und
Achsenbeschriftungen. Wenn der Durchschnitt über 200 °C liegt, soll der Titel
"Bremsscheibentemperatur während der Bremsung (erhöhte Durchschnittstemperatur)"
lauten. Andernfalls bleibt der Titel "Bremsscheibentemperatur während der
Bremsung".

Testen Sie Ihr Skript mit zwei Fällen:

* Testfall 1: Die oben angegebenen Temperaturwerte.
* Testfall 2: Ersetzen Sie die Temperaturwerte durch `[60, 80, 100, 120, 140,
  160, 180]` und beobachten Sie, wie sich der Titel ändert.

Strukturieren Sie Ihren Code mit EVA-Kommentaren.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
Testfall 1: Durchschnitt über 200 °C:
```python
import plotly.express as px

# Eingabe
zeit_s = [0, 0.5, 1.0, 1.5, 2.0, 2.5, 3.0]
temperatur_celsius = [80, 145, 210, 265, 305, 335, 350]

durchschnitt_C = (temperatur_celsius[0] + temperatur_celsius[1] +
                  temperatur_celsius[2] + temperatur_celsius[3] +
                  temperatur_celsius[4] + temperatur_celsius[5] +
                  temperatur_celsius[6]) / 7
SCHWELLENWERT_C = 200

# Verarbeitung
titel = 'Bremsscheibentemperatur während der Bremsung'

if durchschnitt_C > SCHWELLENWERT_C:
    titel = 'Bremsscheibentemperatur während der Bremsung (erhöhte Durchschnittstemperatur)'

fig = px.line(x=zeit_s, y=temperatur_celsius,
              title=titel,
              labels={'x': 'Zeit in Sekunden', 'y': 'Temperatur in °C'})

# Ausgabe
fig.show()
```

Testfall 2: Durchschnitt unter 200 °C (Temperaturwerte ersetzen):
```python
temperatur_celsius = [60, 80, 100, 120, 140, 160, 180]
```

Bei diesen Werten ergibt der Durchschnitt (60+80+100+120+140+160+180)/7 ≈ 120 °C
und der Titel bleibt unverändert.
````

````{admonition} Übung 4.9
:class: tip
Bei einem internationalen Ingenieurbüro werden Messdaten der Bremsscheibe in
verschiedenen Einheiten dokumentiert. Gegeben sind folgende Messwerte:
```python
zeit_s = [0, 0.5, 1.0, 1.5, 2.0, 2.5, 3.0]
temperatur_celsius = [80, 145, 210, 265, 305, 335, 350]
```
Erweitern Sie das Liniendiagramm der Bremsscheibentemperatur um einen Einheiten-Umschalter: Der Benutzer oder die Benutzerin soll beim Programmstart wählen können, ob die Temperatur in Grad Celsius (°C) oder Fahrenheit (°F) angezeigt werden soll. Grad Celsius soll die Voreinstellung sein.

Die Umrechnung von Celsius in Fahrenheit lautet: °F = °C * 9/5 + 32

Berechnen Sie bei Wahl von Fahrenheit jeden Temperaturwert über seinen Index um und speichern Sie die Ergebnisse in einer neuen Liste `temperatur_fahrenheit`. Passen Sie auch die Achsenbeschriftung entsprechend an.

Strukturieren Sie Ihren Code mit EVA-Kommentaren.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import plotly.express as px

# Eingabe
zeit_s = [0, 0.5, 1.0, 1.5, 2.0, 2.5, 3.0]
temperatur_celsius = [80, 145, 210, 265, 305, 335, 350]

einheit = input('Bitte wählen Sie die Einheit (C/F): ')

# Verarbeitung
y_werte = temperatur_celsius
beschriftung_y = 'Temperatur in °C'

if einheit == 'F':
    temperatur_fahrenheit = [temperatur_celsius[0] * 9/5 + 32,
                             temperatur_celsius[1] * 9/5 + 32,
                             temperatur_celsius[2] * 9/5 + 32,
                             temperatur_celsius[3] * 9/5 + 32,
                             temperatur_celsius[4] * 9/5 + 32,
                             temperatur_celsius[5] * 9/5 + 32,
                             temperatur_celsius[6] * 9/5 + 32]
    y_werte = temperatur_fahrenheit
    beschriftung_y = 'Temperatur in °F'

# Ausgabe
fig = px.line(x=zeit_s, y=y_werte,
              title='Bremsscheibentemperatur während der Bremsung',
              labels={'x': 'Zeit in Sekunden', 'y': beschriftung_y})
fig.show()
```

Hinweis: Die Umrechnung der sieben Temperaturwerte über den Index ist korrekt,
aber repetitiv. Im nächsten Kapitel werden wir `for`-Schleifen kennenlernen, mit
denen sich diese Berechnung eleganter und kürzer formulieren lässt ohne jeden
Index einzeln aufzuschreiben.
````

````{admonition} Übung 4.10 (Mini-Projekt)
:class: tip
Sie beobachten den Kursverlauf einer fiktiven Aktie über 7 Handelstage von
Montag bis Sonntag. Die Kurse in Euro sind:
```python
kurse_euro = [120.0, 124.5, 118.3, 115.7, 122.8, 130.4, 112.9]
```

Sie haben die Aktie zu einem Einstiegspreis von 120.00 Euro gekauft.

Schreiben Sie ein Programm, das folgende Fragen beantwortet:

- An welchen Handelstagen lag der Kurs unter dem Einstiegspreis?
- Haben Sie am letzten Handelstag einen Gewinn oder Verlust gemacht, und wie
  hoch ist dieser?

Visualisieren Sie den Kursverlauf abschließend als Liniendiagramm. Das Diagramm
soll auf einen Blick zeigen, ob der Kurs an mindestens einem Tag unter den
Einstiegspreis gefallen ist.

*Anforderungen:*
- Strukturieren Sie mit EVA-Kommentaren.
- Verwenden Sie aussagekräftige Variablennamen.
- Definieren Sie den Einstiegspreis als Konstante.
````
