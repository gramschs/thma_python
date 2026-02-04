---
kernelspec:
  name: python3
  display_name: 'Python 3'
---

# 3.2 Plotly Express

Python kann auch auf schwachbrüstiger Hardware laufen wie beispielsweise auf
dem Raspberry Pi. Ein Grund für die Effizienz von Python ist, dass nicht alle
möglichen Datentypen, Funktionen und Methoden von Beginn an in den Speicher
geladen werden, sondern erst bei Bedarf. Python-Code ist in sogenannte Module
unterteilt.

In diesem Jupyter Notebook werden wir den Modul-Mechanismus anhand des
Plotly-Express-Moduls kennenlernen.

## Lernziele

TODO

## Import von Modulen

Module sind Python-Code, der Konstanten oder Anweisungen (Funktionen, Klassen)
zur Verfügung stellt, die den eigentlichen Python-Kern erweitern. Module müssen
importiert werden, damit der Python-Interpreter diese erweiterten
Funktionalitäten benutzen kann.

Es gibt mehrere Anweisungen, ein Modul zu importieren. Wir verwenden hier den
sogenannten **Alias-Import**. Ein Alias ist eine Abkürzung, in diesem Fall für
den Namen des Moduls. Theoretisch können wir jeden beliebigen Alias verwenden,
in der Praxis haben sich jedoch bestimmte Aliase eingebürgert. Im Fall von
Plotly Express ist `px` der Standard-Alias. Um also das Module Plotly Express
mit dem alias `px` zu importieren, schreiben wir die folgende Code-Zeile:

```{code-cell} python
import plotly.express as px
```

Wird die obige Anweisung ausgeführt, passiert scheinbar nichts. Tatsächlich hat
der Python-Interpreter jedoch das Modul geladen. Die Anweisung `dir(px)` listet
auf, was genau alles importiert wurde.

```{code-cell} python
dir(px)
```

Die Liste der importierten Funktionalitäten ist ganz schön lang. Wenn wir wissen
möchten, was sich hinter den einzelnen Funktionalitäten verbirgt, können wir die
eingebaute Hilfe von Python aufrufen. Dazu suchen wir uns eine Funktionalität
aus, über die wir mehr wissen wollen, und rufen dann die Funktion `help()` auf.
Wenn wir beispielsweise mehr über `scatter` wissen wollen, lautet der Aufruf
folgendermaßen:

```{code-cell} python
help(px.scatter)
```

```{admonition} Alias benutzen
:class: warning
Wenn wir eine Konstante, Funktion oder Klasse aus einem Modul benutzen wollen,
das wir mit einem Alias importiert haben, müssen wir immer den Alias
voranstellen und mit einem Punkt von der Funktionalität abtrennen.
```
