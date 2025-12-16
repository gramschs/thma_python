---
kernelspec:
  name: python3
  display_name: 'Python 3'
---

# 1.2 Jupyter Notebooks und Python als Taschenrechner

In dieser Vorlesung werden wir das Python-Programmieren mit Hilfe von Jupyter
Notebooks lernen. Daher klären wir zunächst, was Jupyter Notebooks sind, und
verwenden anschließend Python als Taschenrechner. Ergebnisse von einfachen
Rechnungen lassen wir uns mit der `print()`-Funktion anzeigen.

## Lernziele

```{admonition} Lernziele
:class: attention
* Sie wissen, was ein **Jupyter Notebook** ist.
* Sie können Python als Taschenrechner benutzen.
* Sie können Ergebnisse von Rechnungen mit **print()** anzeigen.
* Sie wissen, was ein **Argument** einer Anweisung ist.
```

## Was sind Jupyter Notebooks?

Jupyter Notebooks führen Text, Python-Code, Bilder und Videos in einem einzigen
interaktiven digitalen Notizbuch zusammen. Sie gehören zu den bekanntesten
Anwendungen in der Programmierung und werden häufig für Datenanalyse,
maschinelles Lernen, Simulationen und Visualisierungen eingesetzt.

Ein Jupyter Notebook besteht aus einer Abfolge von **Zellen**, in denen Text,
Code oder Grafiken eingebettet werden. Die Zellen können entweder in Python oder
in anderen Programmiersprachen wie R, Julia oder JavaScript geschrieben sein.
Erkennbar sind Jupyter Notebooks an der Dateiendung `.ipynb`.

Die Kombination von Text, Code und Visualisierungen macht Jupyter Notebooks zu
einem besonders geeigneten Werkzeug für das Programmierenlernen: Konzepte
werden im Text erläutert und können direkt in Code-Zellen ausprobiert werden.

```{figure} pics/jupyter_notebook.png
:name: fig_jupyter_notebook
Screenshot eines Jupyter Notebooks mit Text, Python-Code und Ergebnissen des
ausgeführten Python-Codes, das mit der "JupyterLab" geladen wurde (Quelle:
eigene Darstellung; Lizenz [CC BY-NC-SA
4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/))
```

Eine Zelle kann entweder eine Text-Zelle (siehe Screenshot, Schritt 1) oder eine
Code-Zelle (siehe Screenshot, Schritt 2) sein. In Text-Zellen wird die
[Markdown-Formatierung](https://jupyter-notebook.readthedocs.io/en/stable/examples/Notebook/Working%20With%20Markdown%20Cells.html)
verwendet. Um ein Wort fettgedruckt anzuzeigen, schreibt man zum Beispiel
`**fett**`, was als fett dargestellt wird. In Code-Zellen (siehe Screenshot,
Schritt 2 oder 3) können Sie direkt Python-Code eingeben. Eine Code-Zelle wird
ausgeführt, indem Sie auf "Run" klicken (siehe Screenshot, Schritt 4). Danach
erscheint die Ausgabe, die der Python-Interpreter ggf. erzeugt (siehe
Screenshot, Schritt 5). Ergebnisse werden mit "Out" gekennzeichnet.

## Python als Taschenrechner

Bevor wir in die Programmierung einsteigen, benutzen wir Python erst einmal als
Taschenrechner. Im Folgenden sehen Sie, wie die Grundrechenarten in Python
verwendet werden:

Addition:

```{code-cell} python
2+3
```

Subtraktion:

```{code-cell} python
2-3
```

Multiplikation:

```{code-cell} python
2*4
```

Division:

```{code-cell} python
8/2
```

Potenzierung:

```{code-cell} python
3**2
```

Sie können die obigen Code-Zellen verändern, zum Beispiel `2 + 3` in `2 + 5`
ändern. So lernen Sie den Umgang mit Python-Anweisungen kennen.

Wenn Sie dieses Skript als interaktives Jupyter Notebook öffnen, können Sie
direkt in die Zellen klicken und den Code ändern. Falls Sie das Skript online
lesen, klicken Sie bitte auf das Raketensymbol oben rechts und wählen „Live
Code“, um interaktive Zellen zu aktivieren. Beim ersten Start kann dies etwas
dauern.

Um Übungen zu ermöglichen, enthalten manche Zellen nur einen Kommentar als
Platzhalter:

```{code-cell} python
# Geben Sie nach diesem Kommentar Ihren Code ein:
```

Alles was nach dem Hashtag # steht, ist ein **Kommentar**. Kommentare werden von
Python ignoriert und sind nur für uns Menschen gedacht.

Selbstverständlich beherrscht Python auch Klammerregeln. Probieren Sie es aus!

```{admonition} Mini-Übung
:class: tip
Lassen Sie Python den Term $3\cdot (7-10)+5$ berechnen. 
```

```{code-cell} python
# Geben Sie nach diesem Kommentar Ihren Code ein:
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
3 * (7-10) + 5
```
````

## Ausgaben mit print

Bei den obigen Rechenaufgaben wurde automatisch das Ergebnis der Rechnung
angezeigt, sobald die Code-Zelle ausgeführt wurde. Dies ist eine Besonderheit
der Jupyter Notebooks. In einem normalen Python-Programm würde das nicht
funktionieren. Die interaktive Ausgabe der Jupyter Notebooks zeigt außerdem
immer nur das Ergebnis der letzten Zeile an.

Um beliebige Ergebnisse oder Texte gezielt auszugeben, gibt es die
**print()-Funktion**.

```{code-cell} python
print(2)
print(3+3)
```

Das **Argument** wird in runde Klammern hinter den Funktionsnamen `print`
geschrieben. Ein Argument ist sozusagen der Input, der an die Funktion übergeben
wird, damit Python weiß, welcher Wert auf dem Bildschirm angezeigt werden soll.

Das zweite Beispiel in der zweiten Zeile funktioniert genauso. Nur wird diesmal
eine komplette Rechnung als Argument an die `print()`-Funktion übergeben. In dem
Fall rechnet der Python-Interpreter erst den Wert der Rechnung, also `3+3=6` aus
und übergibt dann die `6` an die `print()`-Funktion. Die `print()`-Funktion
wiederum zeigt dann die `6` am Bildschirm an.

Insgesamt zeigt daher der Python-Interpreter erst eine 2 und dann in der
nächsten Zeile eine 6 an.

```{admonition} Mini-Übung
:class: tip
Lassen Sie Python den Term $3:4$ berechnen und geben Sie das Ergebnis mit der
print()-Funktion aus.
```

```{code-cell} python
# Geben Sie nach diesem Kommentar Ihren Code ein:
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
print(3/4)
```
Achtung: In Python wird für die Division `/` verwendet, nicht `:`. Das ist ein
häufiger Fehler.
````

Python kann mit der `print()`-Funktion jedoch nicht nur Zahlen ausgeben, sondern
auch Texte. Ein erster Versuch, einfach den Text als Argument der
`print()`-Funktion zu übergeben, scheitert leider, wie das nächste Beispiel zeigt.

```{code-cell} python
:tags: [raises-exception]
# Achtung, die nachfolgende Code-Zeile enthält einen Fehler!
print(Hallo)
```

Es erscheint eine Fehlermeldung mit dem Fehler: `NameError: name 'Hallo' is not
defined`. Der Grund hierfür ist, dass der Python-Interpreter versucht, eine
sogenannte Variable oder eine Python-Anweisung mit dem Namen `Hallo` zu finden.
Da es aber keines von beiden gibt, kommt die Fehlermeldung, dass `Hallo` nicht
definiert wurde. Um den Text ausgeben zu lassen, werden um den Text einfache
oder doppelte Anführungszeichen gesetzt, wie in dem folgenden Beispiel.

```{code-cell} python
print('Hallo')
```

```{admonition} Mini-Übung
:class: tip
Probieren Sie aus was passiert, wenn Sie die einfachen Anführungszeichen `'`
durch doppelte Anführungszeichen `"` ersetzen. Lassen Sie den Text Hallo Welt
ausgeben.
```

```{code-cell} python
# Geben Sie nach diesem Kommentar Ihren Code ein:
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
print("Hallo Welt")
```
````

In Python sind sowohl einfache als auch doppelte Anführungszeichen erlaubt.
Wenn ein Apostroph im Text vorkommt, sollten Sie doppelte Anführungszeichen
verwenden.

Die `print()`-Funktion kann noch viel mehr, als wir in dieser Einführung
gesehen haben. Wir werden in einem späteren Kapitel im Zusammenhang mit den
sogenannten f-Strings nochmal darauf zurückkommen.

Hinweis: Das folgende Video nutzt eine andere Entwicklungsumgebung (PyCharm) als
wir in dieser Vorlesung. Wir nutzen die Entwicklungsumgebung JupyterLab. Die
grundlegenden Python-Befehle sind jedoch identisch. Fokussieren Sie sich ab
Minute 9 auf die Python-Syntax, nicht auf die Bedienung der Software.

```{dropdown} Video "Dein erstes Python-Programm" von Programmieren Starten
<iframe width="560" height="315" src="https://www.youtube.com/embed/oxXAb8IikHM"
title="YouTube video player" frameborder="0" allow="accelerometer; autoplay;
clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
allowfullscreen></iframe>
```

## Zusammenfassung und Ausblick

In diesem Kapitel haben wir Jupyter Notebooks kennengelernt, Python als
Taschenrechner genutzt und die erste Python-Anweisung `print()` eingesetzt. Im
nächsten Kapitel geht es um das Speichern von Daten und deren Verwaltung.
