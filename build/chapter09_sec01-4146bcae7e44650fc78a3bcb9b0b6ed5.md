---
kernelspec:
  name: python3
  display_name: 'Python 3'
---

# 9.1 NumPy-Arrays

Bisher haben wir Zahlenreihen als Python-Listen gespeichert: In Kapitel 3 haben
wir Listen erzeugt und manipuliert, in Kapitel 5 mit `for`-Schleifen über sie
iteriert. Das funktioniert gut für kleine Datenmengen. Sobald wir aber hunderte
oder tausende von Messwerten verarbeiten und damit rechnen wollen, stoßen Listen
schnell an ihre Grenzen. In Kapitel 6 haben wir bereits das Modul `numpy` für
Zufallszahlen eingesetzt. In diesem Kapitel lernen wir den Kern von NumPy
kennen: das **Array**. Arrays erlauben es, mathematische Operationen direkt auf
ganze Zahlenreihen anzuwenden, ohne eine Schleife schreiben zu müssen.

## Lernziele

```{admonition} Lernziele
:class: attention
* [ ] Sie wissen, was ein **NumPy-Array** ist und wie es sich von einer
  Python-Liste unterscheidet.
* [ ] Sie können ein Array mit `np.array()`, `np.linspace()` und `np.zeros()`
  erzeugen.
* [ ] Sie können **Vektoroperationen** (elementweise Addition, Multiplikation,
  Skalierung) auf Arrays anwenden.
* [ ] Sie können mathematische Funktionen wie `np.sin()` und `np.cos()` auf
  Arrays anwenden.
```

## Was ist ein NumPy-Array?

NumPy (kurz für *Numerical Python*) ist eine Bibliothek für numerische
Berechnungen. Der zentrale Datentyp ist das **Array**, das eine geordnete Folge
von Zahlen desselben Typs umfasst. Wir importieren NumPy wie gewohnt:

```{code-cell} python
import numpy as np
```

Ein Array wird aus einer Liste erzeugt, indem wir `np.array()` übergeben:

```{code-cell} python
geschwindigkeiten = np.array([30, 50, 70, 100, 130])
print(geschwindigkeiten)
```

Mit den Attributen `.shape` und `.dtype` lässt sich ablesen, wie das Array
aufgebaut ist:

```{code-cell} python
print(geschwindigkeiten.shape)   # (5,) - fünf Elemente, eindimensional
print(geschwindigkeiten.dtype)   # int64 - ganzzahliger Typ
```

`.shape` gibt die Abmessungen als Tupel zurück. Ein Tupel ist eine
Datenstruktur, die ähnlich wie eine Liste mehrere Werte zusammenfasst, aber im
Gegensatz zu einer Liste ist ein Tupel unveränderlich. Bei einem
eindimensionalen Array enthält das Tupel nur einen Wert: die Anzahl der
Elemente. `.dtype` zeigt den Datentyp aller Elemente an. Enthält mindestens eine
Zahl einen Dezimalpunkt, wählt NumPy automatisch den Typ `float64`:

```{code-cell} python
messwerte = np.array([1.2, 3.5, 2.8, 4.1])
print(messwerte.dtype)   # float64
```

```{admonition} Array vs. Liste
:class: note
Eine Python-Liste kann beliebig gemischte Typen enthalten: `[1, "Welle", True]`
ist eine gültige Liste. Ein NumPy-Array hingegen enthält **immer nur einen
Datentyp**. Fügt man beim Erzeugen Werte verschiedener Typen ein, wandelt
NumPy sie automatisch in den allgemeinsten gemeinsamen Typ um. Aus
`np.array([1, 2.5, 3])` wird ein Array aus `float64`, da Ganzzahlen verlustfrei
als Fließkommazahlen dargestellt werden können. Dieses Verhalten ist wichtig
zu kennen, um unerwartete Typumwandlungen zu vermeiden.
```

## Arrays erzeugen mit `np.linspace()` und `np.zeros()`

In der Praxis erzeugt man Arrays selten von Hand, sondern nutzt NumPy-Funktionen
dafür. Die wichtigste ist `np.linspace()`. Sie erzeugt eine Folge von Werten,
die gleichmäßig zwischen einem Start- und einem Endwert verteilt sind:

```python
np.linspace(start, stop, num)
```

`start` und `stop` sind der erste und letzte Wert, `num` ist die Anzahl der
Punkte. Anders als `range()` schließt `np.linspace()` den Endwert immer ein.

Als Beispiel erzeugen wir eine Zeitachse für einen 10 Sekunden langen Versuch
mit 6 Messpunkten:

```{code-cell} python
t = np.linspace(0, 10, 6)
print(t)
```

Die sechs Werte `[ 0.  2.  4.  6.  8. 10.]` sind gleichmäßig im Abstand von 2
Sekunden verteilt. In der Simulation und Messtechnik ist das der typische Weg,
eine Zeitachse zu definieren.

Eine zweite nützliche Funktion ist `np.zeros()`. Sie erzeugt ein Array der
gewünschten Länge, das vollständig mit Nullen gefüllt ist, zum Beispiel als
Platzhalter für Berechnungsergebnisse, die noch befüllt werden:

```{code-cell} python
ergebnisse = np.zeros(6)
print(ergebnisse)
```

````{admonition} Mini-Übung
:class: tip
Erzeugen Sie mit `np.linspace()` eine Zeitachse, die von 0 bis $2\pi$ reicht
und 100 gleichmäßig verteilte Punkte enthält. Tipp: `np.pi` ist in NumPy
vordefiniert.

Geben Sie anschließend folgende Informationen aus:
1. die Gesamtzahl der Punkte und
2. den ersten und letzten Wert.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import numpy as np

t = np.linspace(0, 2 * np.pi, 100)

# 1. Anzahl der Punkte
print(t.shape)        # (100,)

# 2. Erster und letzter Wert
print(t[0], t[-1])    # 0.0  6.283185307179586
```

Das Ergebnis zeigt, dass der letzte Wert $2\pi \approx 6.28$ ist und
`np.linspace()` den Endpunkt immer einschließt.
````

## Vektoroperationen

Der größte Vorteil von Arrays gegenüber Listen liegt darin, dass sich
Rechenoperationen direkt auf das gesamte Array anwenden lassen, ohne eine
Schleife zu schreiben. Man spricht von **Vektoroperationen**.

Angenommen, wir möchten eine Reihe von Geschwindigkeitsmesswerten (in km/h) in
m/s umrechnen. Mit einer Liste müsste man eine Schleife schreiben. Mit einem
Array geht das in einer Zeile:

```{code-cell} python
v_kmh = np.array([30.0, 50.0, 70.0, 100.0, 130.0])
v_ms = v_kmh / 3.6
print(v_ms)
```

Die Division durch `3.6` wird auf **jedes Element einzeln** angewendet. Das
gilt genauso für alle anderen Grundrechenarten:

```{code-cell} python
# Kinetische Energie: E = 0.5 * m * v^2 (m = 1500 kg, v in m/s)
m_kg = 1500
E_J = 0.5 * m_kg * v_ms**2
print(E_J)
```

Zwei Arrays derselben Länge können auch elementweise miteinander verrechnet
werden:

```{code-cell} python
a = np.array([1.0, 2.0, 3.0])
b = np.array([4.0, 5.0, 6.0])
print(a + b)    # [ 5.  7.  9.]
print(a * b)    # [ 4. 10. 18.]
```

```{admonition} Plus bei Listen vs. Arrays
:class: note
Bei Python-Listen bewirkt `+` eine **Verkettung**: `[1, 2] + [3, 4]` ergibt
`[1, 2, 3, 4]`. Bei NumPy-Arrays hingegen bedeutet `+` eine **elementweise
Addition**: `np.array([1, 2]) + np.array([3, 4])` ergibt `array([4, 6])`. Diese
unterschiedliche Bedeutung ist eine häufige Fehlerquelle, wenn man zwischen
Listen und Arrays wechselt.
```

````{admonition} Mini-Übung
:class: tip
In einem Schwingungsversuch werden Beschleunigungen in der Einheit $\text{m/s}^2$
gemessen:

```python
a_ms2 = np.array([0.5, 1.2, 2.4, 3.1, 2.8, 1.5, 0.3])
```

1. Rechnen Sie alle Werte in die Einheit $g$ (Erdbeschleunigung) um:
   $a_g = a_{\text{m/s}^2} \,/\, 9.81$.
2. Berechnen Sie die Kraft $F = m \cdot a$ für eine Masse von $m = 5.0\;\text{kg}$
   (Ergebnis in Newton).
3. Geben Sie beide Arrays aus.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import numpy as np

a_ms2 = np.array([0.5, 1.2, 2.4, 3.1, 2.8, 1.5, 0.3])

# 1. Umrechnung in g
a_g = a_ms2 / 9.81
print(a_g)

# 2. Kraft
m_kg = 5.0
F_N = m_kg * a_ms2
print(F_N)
```

Ausgabe:
```
[0.051  0.122  0.245  0.316  0.285  0.153  0.031]
[ 2.5  6.0  12.0  15.5  14.0   7.5   1.5]
```
````

## Mathematische Funktionen: `np.sin()` und `np.cos()`

NumPy stellt alle gängigen mathematischen Funktionen bereit, die direkt auf
Arrays angewendet werden können. Besonders häufig werden in der Ingenieurpraxis
Sinus und Kosinus benötigt, beispielsweise bei der Analyse von Schwingungen oder
rotierenden Systemen.

Die Funktionen `np.sin()` und `np.cos()` erwarten die Winkel im **Bogenmaß
(Radiant)**. Auf ein Array angewendet, berechnen sie den Funktionswert
für jedes Element:

```{code-cell} python
t = np.linspace(0, 2 * np.pi, 7)
y = np.sin(t)

print(t)
print(y)
```

Das Ergebnis ist wiederum ein Array, d.h. alle 7 Sinuswerte werden in einem
Schritt berechnet. Das ist der Schlüssel zur effizienten Simulation: Statt einer
Schleife über einzelne Zeitpunkte berechnen wir den gesamten Signalverlauf auf
einmal.

In der Praxis wählt man für glatte Kurven deutlich mehr Punkte:

```{code-cell} python
t = np.linspace(0, 2 * np.pi, 500)
y_sin = np.sin(t)
y_cos = np.cos(t)
```

Mit diesen Arrays lassen sich in Kapitel 9.2 direkt Diagramme erzeugen, ohne
eine einzige Schleife zu schreiben.

````{admonition} Mini-Übung
:class: tip
Erzeugen Sie eine Zeitachse `t` von $0$ bis $2\pi$ mit 100 Punkten und
berechnen Sie daraus ein Array `y` mit den Kosinuswerten.

Prüfen Sie anschließend das Ergebnis:
1. Geben Sie den ersten Wert `y[0]` gerundet auf 1 Nachkommastelle aus –
   er sollte `1.0` sein, da $\cos(0) = 1$.
2. Geben Sie den letzten Wert `y[-1]` gerundet auf 1 Nachkommastelle aus –
   er sollte ebenfalls `1.0` sein, da $\cos(2\pi) = 1$.

Tipp: Verwenden Sie `round(wert, 1)` für die Rundung.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import numpy as np

t = np.linspace(0, 2 * np.pi, 100)
y = np.cos(t)

print(round(y[0], 1))    # 1.0
print(round(y[-1], 1))   # 1.0
```

Beide Werte sind `1.0`, was die Erwartung bestätigt. Da Fließkommazahlen im
Computer nie exakt dargestellt werden, ist `y[-1]` nicht exakt `1.0`, sondern
liegt sehr knapp darunter. Die Rundung auf eine Nachkommastelle zeigt aber den
erwarteten Wert.
````

## Zusammenfassung und Ausblick

In diesem Kapitel haben wir NumPy-Arrays als leistungsfähige Alternative zu
Python-Listen kennengelernt. Arrays speichern stets Werte desselben Datentyps
und erlauben es, Rechenoperationen und mathematische Funktionen direkt auf
ganze Zahlenreihen anzuwenden – ohne Schleifen und deutlich schneller als
Listen. Mit `np.linspace()` lassen sich gleichmäßig verteilte Wertebereiche
erzeugen, `np.zeros()` liefert vorbelegte Platzhalter-Arrays. Vektoroperationen
wie Skalarmultiplikation oder elementweise Addition funktionieren intuitiv, aber
Vorsicht: `+` bedeutet bei Arrays etwas völlig anderes als bei Listen. Im
nächsten Kapitel verbinden wir diese Grundlagen mit Plotly Express, um
physikalische Vorgänge wie Kinematik und Schwingungen zu visualisieren.
