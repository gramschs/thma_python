---
kernelspec:
  name: python3
  display_name: 'Python 3'
---

# Übungen

````{admonition} Übung 2.1
:class: tip
Betrachten Sie die folgenden beiden Code-Zeilen:

```python
print(5 + 3)
print('5' + '3')
```

1. Sagen Sie vorher, was jeweils ausgegeben wird.
2. Führen Sie den Code in der nächsten Code-Zelle aus und überprüfen Sie Ihre
   Vorhersage.
3. Erklären Sie, warum die Ausgaben unterschiedlich sind.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
1. Vorhersage

  * `print(5 + 3)` gibt `8` aus
  * `print('5' + '3')` gibt `53` aus

2. Ausführung Beim Ausführen des Codes sehen Sie genau diese Ausgaben.

3. Erklärung

  * In der ersten Zeile werden zwei **Integer** (Ganzzahlen) addiert. Der
    `+`-Operator führt eine mathematische Addition durch: 5 + 3 = 8
  * In der zweiten Zeile werden zwei **Strings** (Zeichenketten) verkettet. Die
    Anführungszeichen machen aus den Zahlen Texte. Der `+`-Operator hängt bei
    Strings die Zeichenketten hintereinander: '5' + '3' = '53'

Wichtige Erkenntnis: Der Datentyp bestimmt, wie Operationen durchgeführt werden.
Derselbe Operator (`+`) verhält sich bei Zahlen und Strings völlig
unterschiedlich!
````

```{admonition} Übung 2.2
:class: tip
Ein Stahlträger hat eine Länge von 3.5 m und wiegt pro Meter 25.4 kg.

1. Speichern Sie die Länge in einer Variable `laenge` und das Gewicht pro Meter
   in einer Variable `gewicht_pro_meter`.
2. Berechnen Sie das Gesamtgewicht des Trägers mit der Formel: Gesamtgewicht =
   Länge · Gewicht pro Meter.
3. Geben Sie das Ergebnis mit `print()` aus.
```

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
# Variablen initialisieren
laenge = 3.5
gewicht_pro_meter = 25.4

# Berechnung
gesamtgewicht = laenge * gewicht_pro_meter

# Ausgabe
print(gesamtgewicht)
```

Alternative Ausgabe mit Text und Einheit:
```python
print('Das Gesamtgewicht beträgt', gesamtgewicht, 'kg')
```
Das Ergebnis ist 88.9 kg.
````

````{admonition} Übung 2.3
:class: tip
Gegeben sind folgende Variablen für ein Bauteil:

```python
bauteil_typ = "Schraube"
material = "Edelstahl"
norm = "DIN 933"
durchmesser = "M8"
```

1. Verketten Sie diese vier Strings mit dem `+`-Operator zu einem vollständigen
   Satz nach folgendem Muster: `Bauteil: [Typ], Material: [Material], Norm:
   [Norm], Durchmesser: [Durchmesser]`
2. Geben Sie den zusammengesetzten String mit `print()` aus.

Tipp: Vergessen Sie nicht die Leerzeichen und Kommas zwischen den Textteilen!
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
# gegebene Variablen
bauteil_typ = "Schraube"
material = "Edelstahl"
norm = "DIN 933"
durchmesser = "M8"

# String-Verkettung
beschreibung = "Bauteil: " + bauteil_typ + ", Material: " + material + ", Norm: " + norm + ", Durchmesser: " + durchmesser

# Ausgabe
print(beschreibung)
```

Alternative kürzere Lösung (direkt in `print()`):
```python
print("Bauteil: " + bauteil_typ + ", Material: " + material + ", Norm: " + norm + ", Durchmesser: " + durchmesser)
```
````

```{admonition} Übung 2.4
:class: tip
Schreiben Sie ein Programm, das nacheinander nach folgenden Informationen fragt:

1. Vorname
2. Studiengang
3. Lieblingsfach

Das Programm soll anschließend einen vollständigen Satz ausgeben: "Hallo
[Vorname], du studierst [Studiengang] und dein Lieblingsfach ist
[Lieblingsfach]."

Hinweis: Verwenden Sie die `input()`-Funktion und String-Verkettung mit `+`.
```

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
# Eingabe
vorname = input('Wie ist dein Vorname? ')
studiengang = input('Was studierst du? ')
lieblingsfach = input('Was ist dein Lieblingsfach? ')

# Ausgabe
print('Hallo ' + vorname + ', du studierst ' + studiengang + ' und dein Lieblingsfach ist ' + lieblingsfach + '.')
```
Beispiel-Ausgabe: Wenn die Eingaben "Anna", "Maschinenbau" und
"Werkstofftechnik" sind, lautet die Ausgabe: 
``` 
Hallo Anna, du studierst Maschinenbau und dein Lieblingsfach ist Werkstofftechnik.
```
````

```{admonition} Übung 2.5
:class: tip
Schreiben Sie ein Programm, das die Fläche eines rechteckigen Bauteils
berechnet.

1. Fragen Sie nach der Länge des Bauteils in Metern.
2. Fragen Sie nach der Breite des Bauteils in Metern.
3. Berechnen Sie die Fläche mit der Formel: Fläche = Länge · Breite.
4. Geben Sie das Ergebnis aus: "Die Fläche beträgt \[Ergebnis\] m^2."

Hinweis: Verwenden Sie `float()`, um die Eingaben in Fließkommazahlen
umzuwandeln, und `str()`, um die berechnete Fläche in der Ausgabe einzufügen.
```

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
# Eingabe
laenge = float(input('Geben Sie die Länge in Metern ein: '))
breite = float(input('Geben Sie die Breite in Metern ein: '))

# Verarbeitung
flaeche = laenge * breite

# Ausgabe
print('Die Fläche beträgt ' + str(flaeche) + ' m^2.')
```

Beispiel-Ausgabe:
Bei Eingaben 3.5 und 2.4 lautet die Ausgabe:
```
Die Fläche beträgt 8.4 m^2.
```
````

```{admonition} Übung 2.6
:class: tip
Gegeben ist folgende Liste von Variablennamen:

1. `temperatur_celsius`
2. `3messung`
3. `Kraft-Newton`
4. `x`
5. `geschwindigkeit_m_pro_s`
6. `länge`
7. `print`
8. `MeineVariable`
9. `a`
10. `querschnittsflaeche_m2`

Analysieren Sie jeden Variablennamen und entscheiden Sie:
- *ungültig*: Welche Namen sind in Python nicht erlaubt? Begründen Sie, warum.
- *ungeschickt*: Welche Namen sind zwar erlaubt, aber in der Praxis schlecht
  gewählt? Begründen Sie, warum.
- *gut*: Welche Namen sind empfehlenswert?

Hinweis: Denken Sie an die Regeln, d.h. keine Zahlen am Anfang, keine Umlaute,
keine Bindestriche, keine Schlüsselwörter, aussagekräftige Namen bevorzugen.
```

```{admonition} Lösung
:class: tip
:class: dropdown
| Variablenname | Einordnung | Begründung |
| ------------- | ---------- | ---------- |
| `temperatur_celsius` | gut | aussagekräftig, snake_case, mit Einheit |
| `3messung` | ungültig | Variable beginnt mit einer Zahl; korrekt: `messung3` oder `messung_3` |
| `Kraft-Newton` | ungültig | Bindestrich (Minus-Zeichen) ist nicht erlaubt; korrekt: `kraft_newton` |
| `x` | ungeschickt | zu kurz, nicht aussagekräftig; nur in sehr kurzen Programmen akzeptabel |
| `geschwindigkeit_m_pro_s` | gut | sehr aussagekräftig, snake_case, enthält Einheit |
| `länge` | ungültig | Umlaut ist nicht erlaubt; korrekt: `laenge` |
| `print` | ungültig | Schlüsselwort von Python, darf nicht als Variablenname verwendet werden |
| `MeineVariable` | ungeschickt | verwendet UpperCamelCase statt snake_case (empfohlen für Python-Variablen) |
| `a` | ungeschickt | zu kurz, nicht aussagekräftig |
| `querschnittsflaeche_m2` | gut | aussagekräftig, snake_case, mit Einheit (m2 für m²) |
```

````{admonition} Übung 2.7
:class: tip
Gegeben ist folgender Code:

```python
spannung = 230
spannung = spannung * 2
spannung = spannung - 100
spannung = spannung / 3
print(spannung)
```
1. Führen Sie den Code *gedanklich* Schritt für Schritt aus und notieren Sie
   nach jeder Zeile den aktuellen Wert der Variable `spannung`.
2. Erstellen Sie eine Tabelle mit zwei Spalten: "nach Zeile" und "Wert von
   spannung"
3. Führen Sie den Code anschließend in der Code-Zelle aus und überprüfen Sie
   Ihre Vorhersage.

Hinweis: Denken Sie daran, dass der Zuweisungsoperator `=` in zwei Schritten
arbeitet: Erst wird die rechte Seite berechnet, dann wird das Ergebnis der
Variable auf der linken Seite zugewiesen.
````

```{code-cell} python
# Code-Zelle
```

```{admonition} Lösung
:class: tip
:class: dropdown

Schrittweise Ausführung:

| nach Zeile | Wert von spannung | Berechnung |
|------------|-------------------|------------|
| `spannung = 230` | 230 | Initialisierung |
| `spannung = spannung * 2` | 460 | 230 * 2 = 460 |
| `spannung = spannung - 100` | 360 | 460 - 100 = 360 |
| `spannung = spannung / 3` | 120.0 | 360 / 3 = 120.0 |

Endergebnis: `120.0`

Erklärung: Der Zuweisungsoperator arbeitet immer nach dem gleichen Prinzip:
1. Berechne den Wert auf der rechten Seite (dabei wird der alte Wert der
   Variable verwendet).
2. Weise das Ergebnis der Variable auf der linken Seite zu (überschreibt den
   alten Wert).

Beachten Sie: Das Ergebnis ist 120.0 (Float), nicht 120 (Integer), weil die
Division `/` in Python immer ein Float-Ergebnis liefert.
```



