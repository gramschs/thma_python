---
kernelspec:
  name: python3
  display_name: 'Python 3'
---

# Plotly Express

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

Nachdem wir das Modul mit einem Alias importiert haben, verwenden wir diesen
Alias, um auf die Funktionen und Klassen des Moduls zuzugreifen:

```{code-cell} ipython3
x = np.pi
print(x)
```