# Übungen

````{admonition} Mini-Übung
:class: tip
Der folgende Code berechnet die Zugspannung in einem Stahlseil. Die
Variablennamen sind aber schlecht gewählt. Schreiben Sie den Code mit
aussagekräftigen Variablennamen neu. Tipp: f steht für Kraft in Newton, a für
Querschnittsfläche in m², s für Spannung.

```python
f = 12000
a = 0.0008
s = f / a
print(s)
```
````

````{admonition} Lösung
:class: tip
:class: dropdown
```python
kraft_newton = 12000
querschnittsflaeche_m2 = 0.0008
spannung_pascal = kraft_newton / querschnittsflaeche_m2
print(spannung_pascal)
```
````

```{admonition} Mini-Übung
:class: tip
Schreiben Sie ein Programm, das nacheinander nach zwei ganzen Zahlen fragt.
Anschließend gibt das Programm eine 1x1-Aufgabe mit Lösung aus.

Beispiel: Die Benutzerin wählt die Zahlen 3 und 5. Das Programm gibt aus: `3 * 5
= 15`.

Testen Sie anschließend Ihr Programm mit 1x1-Aufgaben, die Sie sich selbst
ausdenken.
```

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
# Eingabe der beiden Zahlen durch Abfrage und direkt Umwandlung
zahl1 = int(input('Bitte geben Sie die erste Zahl ein: '))
zahl2 = int(input('Bitte geben Sie die zweite Zahl ein: '))

# Verarbeitung
produkt = zahl1 * zahl2

# Ausgabe
print(str(zahl1) + ' * ' + str(zahl2) + ' = ' + str(produkt))
```
````