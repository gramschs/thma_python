---
kernelspec:
  name: python3
  display_name: 'Python 3'
---

# Übungen

````{admonition} Übung 5.1 (✩)
:class: tip
Gegeben ist folgende Liste mit Werkstoffen:

```python
materialien = ["Stahl", "Aluminium", "Titan", "Kupfer"]
```

Schreiben Sie ein Programm, das mit einer for-Schleife jedes Material
nummeriert ausgibt. Die Ausgabe soll folgendes Format haben:

```
Material 1: Stahl
Material 2: Aluminium
Material 3: Titan
Material 4: Kupfer
```

Hinweis: Verwenden Sie eine zusätzliche Zählvariable, die Sie vor der Schleife
auf 1 setzen und in jedem Schleifendurchgang um 1 erhöhen.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
materialien = ["Stahl", "Aluminium", "Titan", "Kupfer"]

nummer = 1
for material in materialien:
    print("Material " + str(nummer) + ": " + material)
    nummer = nummer + 1
```

Ausgabe:
```
Material 1: Stahl
Material 2: Aluminium
Material 3: Titan
Material 4: Kupfer
```

Erklärung: Die Variable `nummer` wird vor der Schleife auf `1` initialisiert.
In jedem Schleifendurchgang nimmt die Schleifenvariable `material` den nächsten
Wert aus der Liste an. Da `nummer` eine Ganzzahl (Integer) ist, muss sie mit
`str()` in einen String umgewandelt werden, bevor sie mit `+` verkettet werden
kann. Am Ende jedes Durchgangs wird `nummer` um 1 erhöht, damit beim nächsten
Durchgang die nächste Nummer ausgegeben wird.
````

````{admonition} Übung 5.2 (✩)
:class: tip
Schreiben Sie ein Programm, das den Benutzer oder die Benutzerin nach einer
ganzen Zahl fragt und anschließend das kleine Einmaleins für diese Zahl ausgibt.

Beispiel: Wenn die Zahl `3` eingegeben wird, soll die Ausgabe so aussehen:

```
1 x 3 = 3
2 x 3 = 6
3 x 3 = 9
4 x 3 = 12
5 x 3 = 15
6 x 3 = 18
7 x 3 = 21
8 x 3 = 24
9 x 3 = 27
10 x 3 = 30
```

Verwenden Sie eine for-Schleife mit `range()`.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
# Eingabe
zahl = int(input("Für welche Zahl soll das Einmaleins ausgegeben werden? "))

# Verarbeitung und Ausgabe
for i in range(1, 11):
    ergebnis = i * zahl 
    print(str(i) + " x " + str(zahl) + " = " + str(ergebnis))
```
Erklärung: `range(1, 11)` erzeugt die Zahlen 1 bis 10. Die obere Grenze `11`
gehört dabei nicht mehr zur Folge, da `range()` immer bis zur stop-Zahl minus 1
zählt. In jedem Schleifendurchgang nimmt `i` nacheinander die Werte 1, 2, ...,
10 an. Das Produkt `zahl * i` wird in der Variablen `ergebnis` gespeichert und
anschließend ausgegeben.
````

```{admonition} Übung 5.3 (✩)
:class: tip
Bei rotierenden Maschinenteilen (z. B. Turbinenschaufeln oder Kupplungsscheiben)
wirkt auf jedes Bauteil eine Fliehkraft. Diese hängt von der Drehzahl der
Maschine ab und ist bei der Auslegung von Bauteilen zu berücksichtigen.

Die Fliehkraft $F$ in Newton berechnet sich nach der Formel:

$$F = m \cdot \omega^2 \cdot r$$

Dabei ist $\omega$ die Winkelgeschwindigkeit in rad/s, die sich aus der Drehzahl
$n$ in U/min wie folgt ergibt:

$$\omega = \frac{2 \pi \cdot n}{60}$$

Gegeben sind folgende Werte:

| Größe | Wert |
| ----- | ---- |
| Masse $m$ | 2.0 kg |
| Radius $r$ | 0.3 m |
| Kreiszahl $\pi$ | 3.14159 |

Berechnen Sie die Fliehkraft für Drehzahlen von 500 U/min bis 3000 U/min in
500er-Schritten und geben Sie die Ergebnisse aus.
```

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
# Eingabe
PI = 3.14159
m_kg = 2.0
r_m = 0.3

# Verarbeitung und Ausgabe
for n in range(500, 3001, 500):
    omega = 2 * PI * n / 60
    F_N = m_kg * omega**2 * r_m
    print("n = " + str(n) + " U/min,  F = " + str(F_N) + " N")
```

Ausgabe:
```
n = 500 U/min,  F = 1644.918...
n = 1000 U/min,  F = 6579.672...
n = 1500 U/min,  F = 14804.262...
n = 2000 U/min,  F = 26319.688...
n = 2500 U/min,  F = 41124.513...
n = 3000 U/min,  F = 59219.297...
```

Erklärung: `PI` wird als Konstante mit dem Wert 3.14159 definiert und in der
Berechnung der Winkelgeschwindigkeit `omega` verwendet. Großbuchstaben für
Konstanten sind eine bewährte Konvention in der Programmierung, die auf den
ersten Blick deutlich macht, dass sich dieser Wert im Programm nicht ändert.
`range(500, 3001, 500)` erzeugt die Zahlen 500, 1000, 1500, 2000, 2500, 3000 –
die obere Grenze muss `3001` lauten, damit 3000 noch enthalten ist. Die Ausgabe
enthält viele Nachkommastellen, da Python mit Gleitkommazahlen rechnet. In einem
späteren Kapitel werden wir NumPy kennenlernen, das u. a. eine präzisere
Kreiszahl `numpy.pi` sowie komfortablere Möglichkeiten zur Berechnung solcher
Wertetabellen bereitstellt.
````
