---
kernelspec:
  name: python3
  display_name: 'Python 3'
---

# Übungen

```{admonition} Übung 1.1
:class: tip
Installieren Sie Anaconda auf Ihrem System. Starten Sie JupyterLab und erstellen
Sie ein neues Notebook. Bei Problemen konsultieren Sie die
Installationsanleitung.
```

```{admonition} Übung 1.2
:class: tip
Benutzen Sie Python als Taschenrechner. Fügen Sie dazu diesem Jupyter Notebook
eine Code-Zelle hinzu und lassen Sie die folgenden Ausdrücke berechnen:
* 2 + 3
* 2 - 3
* 4 * 5
* 16 / 4
* 16 / 3
* 5**2
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
print(2+3)
print(2-3)
print(4*5)
print(16/4)
print(16/3)
print(5**2)
```
````

```{admonition} Übung 1.3
:class: tip
In der vorhergehenden Aufgabe haben Sie den Ausdruck `5**2` berechnen lassen.
Fügen Sie jetzt eine Markdown-Zelle ein. Schreiben Sie auf, was Ihrer Vermutung
nach der `**`-Operator für eine Bedeutung hat. Recherchieren Sie anschließend im
Internet, nach seiner Bedeutung und vergleichen Sie Ihre Antwort mit der Recherche.
Fügen Sie die Internetseite als URL in die Markdown-Zelle ein.
```

````{admonition} Lösung
:class: tip
:class: dropdown
Die beiden Sterne `**` stehen für das Potenzieren. Eine kurze Beschreibung findet sich hier:
[https://www.w3schools.com/python/gloss_python_arithmetic_operators.asp]
````

```{admonition} Übung 1.4
:class: tip
Speichern Sie das bearbeitete Jupyter Notebook unter einem anderen Namen ab.
```

````{admonition} Lösung
:class: tip
:class: dropdown
Sehen Sie sich den folgenden Screencast an.
![Screencast des Save-as-Dialogs](pics/solution_01_04.mp4)
````

```{admonition} Übung 1.5
:class: tip
Probieren Sie bewusst falsche Python-Anweisungen aus und beobachten Sie die
Fehlermeldungen.

* Geben Sie `print(Hallo Welt)` ein (ohne Anführungszeichen).
* Versuchen Sie `2 +* 3` (falsche Operatorenkombination).
* Schreiben Sie `Print(5)` (großes P) .

Notieren Sie in einer Markdown-Zelle, welche Fehlermeldungen erscheinen und was
sie bedeuten könnten.
```

```{admonition} Lösung
:class: tip
:class: dropdown
* `print(Hallo Welt)` ohne Anführungszeichen führt zu der Fehlermeldung
  `SyntaxError: invalid syntax`. Syntax ist der Fachbegriff für die Grammatik
  einer Sprache. Diese Anweisung ist ungültig, weil `Hallo Welt` nicht als
  String gekennzeichnet wurde, also in Anführungszeichen gesetzt wurde.
* Die Anweisung `2 +* 3` führt ebenfalls zu einem Grammatikfehler, also
  `SyntaxError: invalid syntax`.
* Die Anweisung `Print(5)` führt zu einem Namensfehler `NameError: name 'Print'
  is not defined`. Python achtet penibel auf Groß- und Kleinschreibung. Den
  Befehl `Print()` mit einem großem P kennt Python daher nicht und meldet
  deshalb den NameError.
```

````{admonition} Übung 1.6
:class: tip
Erstellen Sie eine Code-Zelle mit folgendem Inhalt:
```python
# Das ist ein Kommentar
print(7 + 3)  # Hier wird 7 + 3 berechnet
# print(5 * 2)
print(8 - 2)
```
Führen Sie die Zelle aus. Erklären Sie in einer Markdown-Zelle, warum manche
Zeilen ausgeführt werden und andere nicht.
````

```{admonition} Lösung
:class: tip
:class: dropdown
Es werden nur die Zeilen ausgeführt, in denen **kein** Kommentarzeichen `#`
steht.
```

```{admonition} Übung 1.7
:class: tip
Berechnen Sie folgende Ausdrücke und vergleichen Sie die Ergebnisse:
* `2 + 3 * 4`
* `(2 + 3) * 4`
* `2**3*4`
* `2**(3*4)`

Schreiben Sie in eine Markdown-Zelle, welche Regeln Python für die Reihenfolge
der Operationen befolgt.
```

```{admonition} Lösung
:class: tip
:class: dropdown
Es gelten die folgenden Regeln für die Reihenfolge der Operationen:
* Punkt- vor Strichrechnung (als erst `*` und `\` vor `+` und `-`).
* Klammern werden immer zuerst berechnet.
* Potenzen werden vor `+`, `-`, `*`, `\` berechnet. Erst wird $2^3$ berechnet,
  was 8 ergibt, und dann mit 4 multipliziert, so dass das Endergebnis 32 ist.
  Das Endergebnis ist *nicht* $2^{12} = 4096$.
* Klammern werden weiterhin zuerst berechnet, also vor der Potenzierung
  ausgewertet. Das Ergebnis ist 4096.
```

```{admonition} Übung 1.8
:class: tip
Experimentieren Sie mit der print()-Funktion:

* `print("Mein Name ist", "Max")`
* `print("Das Ergebnis ist:", 5*6)`
* `print(2, 4, 6, 8)`

Was beobachten Sie, wenn print() mehrere Argumente erhält?
```

```{admonition} Lösung
:class: tip
:class: dropdown
Werden der `print()`-Anweisung zwei Argumente übergeben, werden beide Argumente
in einer Zeile angezeigt. Das Komma, das die beiden Argumente trennt, wird nicht
ausgegeben. Aus  `print("Mein Name ist", "Max")` wird also der Text `Mein Name
ist Max`. Das funktioniert auch bei Zahlen und sogar Rechnungen. Aus `print("Das
Ergebnis ist:", 5*6)` wird `Das Ergebnis ist: 30`.

Python lässt in der `print()`-Funktion beliebig viele Argumente zu. Auch
beispielsweise vier Argumente wie in der Anweisung `print(2, 4, 6, 8)`
funktionieren, die Ausgabe ist `2 4 6 8`.
```

```{admonition} Übung 1.9
:class: tip
Berechnen Sie mit Python typische Ingenieursaufgaben, z.B.

* den Umfang eines Kreises mit Radius 5 cm ($U = 2\pi r$, verwenden Sie $\pi
  \approx 3.14159$),
* die Fläche eines Rechtecks mit Länge 12 m und Breite 8 m oder
* die Geschwindigkeit eines Autos bei gleichförmiger Bewegung mit Weg 150 km in
  Zeit 2.5 h.

Verwenden Sie `print()` um die Ergebnisse mit beschreibendem Text auszugeben.
Wie kann Ihnen die vorherige Aufgabe dabei helfen?
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
print('Der Umfang des Kreises mit r =', 5, 'ist', 2 * 5 * 3.14159, '.')
print('Die Fläche des Rechtecks mit Seite a =', 12, 'und Seite b =', 8, 'ist', 12*8, '.')
print('Die Geschwindigkeit ist', 150/2.5, 'km/h, wenn s =', 150, 'km und t =', 2.5, 'h .')
```
`````
