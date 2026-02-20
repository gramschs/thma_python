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
