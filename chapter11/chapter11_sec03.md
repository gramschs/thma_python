---
kernelspec:
  name: python3
  display_name: 'Python 3'
---

# Übungen

````{admonition} Übung 11.1 (✩)
:class: tip
In dieser Aufgabe arbeiten wir mit simulierten Zugversuchsdaten aus der Datei
`zugversuch.csv`. Der Datensatz enthält 150 Messungen an Zugproben aus drei
Werkstoffen. Die Probenlänge beträgt jeweils 100 mm.


1. Lesen Sie die Datei ein und geben Sie die ersten fünf Zeilen aus.
2. Wie viele Zeilen und Spalten hat der Datensatz? Wie viele Messungen gibt es
   pro Werkstoff? Verwenden Sie `.value_counts()`.
3. Erstellen Sie ein Streudiagramm mit `Verlaengerung_mm` auf der x-Achse und
   `Kraft_N` auf der y-Achse. Färben Sie die Punkte nach `Werkstoff` ein. Was
   beobachten Sie?
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import pandas as pd
import plotly.express as px

# Eingabe
df = pd.read_csv("zugversuch.csv")

# 1. Erste Zeilen
print(df.head())

# 2. Struktur und Verteilung
print(df.shape)
print(df["Werkstoff"].value_counts())

# 3. Streudiagramm
fig = px.scatter(data_frame=df,
                 x="Verlaengerung_mm",
                 y="Kraft_N",
                 color="Werkstoff",
                 title="Zugversuch: Kraft in Abhängigkeit der Verlängerung")
fig.show()
```

Der Datensatz hat 150 Zeilen und 4 Spalten, mit je 50 Messungen pro Werkstoff.
Im Streudiagramm sind drei klar getrennte Punktwolken erkennbar, die jeweils
einen linearen Verlauf zeigen. Stahl hat die steilste Kennlinie (höchste
Steifigkeit), da bei gleicher Verlängerung die größte Kraft erforderlich ist.
Aluminium hat die flachste Kennlinie, da es den niedrigsten E-Modul besitzt und
sich bei gleicher Kraft am stärksten verlängert.
````

````{admonition} Übung 11.2 (✩)
:class: tip
Berechnen Sie aus den vorhandenen Spalten zwei neue technische Kenngrößen und
visualisieren Sie die Ergebnisse.

1. Berechnen Sie die **Spannung** in MPa und speichern Sie sie in einer neuen
   Spalte `Spannung_MPa`:
   $$\sigma = \frac{F}{A}$$
   wobei $F$ die Kraft in N und $A$ der Querschnitt in mm² ist. Das Ergebnis
   hat die Einheit N/mm² = MPa.

2. Berechnen Sie die **Dehnung** in Prozent und speichern Sie sie in einer
   neuen Spalte `Dehnung_Proz`:
   $$\varepsilon = \frac{\Delta L}{L_0} \cdot 100$$
   mit $\Delta L$ als Verlängerung in mm und $L_0 = 100$ mm als Ausgangslänge.

3. Erstellen Sie einen Boxplot der Spalte `Spannung_MPa` gruppiert nach
   `Werkstoff`. Interpretieren Sie die Ausgabe: Warum unterscheiden sich die
   Verteilungen kaum zwischen den Werkstoffen?
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import pandas as pd
import plotly.express as px

# Eingabe
L0 = 100.0  # mm
df = pd.read_csv("zugversuch.csv")

# Verarbeitung
df["Spannung_MPa"] = df["Kraft_N"] / df["Querschnitt_mm2"]
df["Dehnung_Proz"] = (df["Verlaengerung_mm"] / L0) * 100

# Ausgabe
fig = px.box(data_frame=df,
             x="Werkstoff",
             y="Spannung_MPa",
             title="Spannungsverteilung nach Werkstoff")
fig.show()
```

Die Spannung hängt nur von Kraft und Querschnitt ab, nicht vom Werkstoff. Da
alle Proben ähnliche Querschnitte haben und derselbe Kraftbereich für alle drei
Werkstoffe verwendet wurde, sind die Spannungsverteilungen nahezu identisch.
Der Werkstoff bestimmt nicht die Spannung, sondern wie stark sich die Probe
unter dieser Spannung verformt, also die Dehnung.

In diesem simulierten Datensatz wurde für alle Werkstoffe ein ähnlicher
Kraftbereich gewählt. In realen Versuchen können sich die maximalen Kräfte je
nach Werkstoff deutlich unterscheiden.
````

````{admonition} Übung 11.3 (✩✩)
:class: tip
Berechnen Sie eine lineare Regressionsgerade für **Stahl** und zeichnen Sie sie
in ein Streudiagramm ein.


1. Filtern Sie den Datensatz auf den Werkstoff `"Stahl"` und extrahieren Sie
   `Verlaengerung_mm` und `Kraft_N` als NumPy-Arrays.
2. Berechnen Sie mit `np.polyfit()` die Koeffizienten der Regressionsgeraden
   und geben Sie Steigung und R² aus.
3. Berechnen Sie mit `np.linspace()` ein Werte-Array `x_fit` vom minimalen
   bis maximalen Verlängerungswert (200 Punkte) und die zugehörigen
   Vorhersagewerte `y_fit`.
4. Erstellen Sie das Streudiagramm und fügen Sie die Regressionsgerade mit
   `fig.add_scatter()` hinzu. Geben Sie R² im Titel aus.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import pandas as pd
import numpy as np
import plotly.express as px

# Eingabe
df = pd.read_csv("zugversuch.csv")
df_stahl = df[df["Werkstoff"] == "Stahl"]

x = df_stahl["Verlaengerung_mm"].values
y = df_stahl["Kraft_N"].values

# Verarbeitung
koeff = np.polyfit(x, y, 1)
gerade = np.poly1d(koeff)
R2 = np.corrcoef(x, y)[0, 1]**2

x_fit = np.linspace(x.min(), x.max(), 200)
y_fit = gerade(x_fit)

# Ausgabe
print(f"Steigung: {koeff[0]:.0f} N/mm")
print(f"R²:       {R2:.4f}")

fig = px.scatter(data_frame=df_stahl,
                 x="Verlaengerung_mm",
                 y="Kraft_N",
                 opacity=0.6,
                 title=f"Zugversuch Stahl | R² = {R2:.4f}")
fig.add_scatter(x=x_fit, y=y_fit, mode="lines", name="Regression")
fig.show()
```

Da `zugversuch.csv` keine fehlenden Werte enthält, können wir hier auf
`.dropna()` verzichten.

R² ≈ 0.996 zeigt einen sehr engen linearen Zusammenhang, was dem Hookeschen
Gesetz im elastischen Bereich entspricht. Die Steigung beschreibt die
geometrieabhängige Steifigkeit der Probe (nicht den Materialkennwert E-Modul).
Pro Millimeter zusätzlicher Verlängerung nimmt die Kraft um diesen Betrag zu.
````

````{admonition} Übung 11.4 (✩✩)
:class: tip
Vergleichen Sie die Regressionsgeraden aller drei Werkstoffe.

Berechnen Sie für jeden der drei Werkstoffe `"Stahl"`, `"Aluminium"` und
`"Titan"` die Steigung der Regressionsgeraden (Kraft über Verlängerung) und R².
Geben Sie die Ergebnisse als formatierte Tabelle aus:

```
Werkstoff  |  Steigung (N/mm)  |  R²
-----------|-------------------|-------
Stahl      |      1.05e+05     | 0.9958
Aluminium  |      ...          | ...
Titan      |      ...          | ...
```

Welcher Werkstoff hat die größte Steigung? Was bedeutet das physikalisch?
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import pandas as pd
import numpy as np

# Eingabe
df = pd.read_csv("zugversuch.csv")

# Verarbeitung und Ausgabe
print(f"{'Werkstoff':<12} | {'Steigung (N/mm)':>17} | {'R²':>6}")
print("-" * 42)

for mat in ["Stahl", "Aluminium", "Titan"]:
    sub = df[df["Werkstoff"] == mat]
    x = sub["Verlaengerung_mm"].values
    y = sub["Kraft_N"].values
    koeff = np.polyfit(x, y, 1)
    R2 = np.corrcoef(x, y)[0, 1]**2
    print(f"{mat:<12} | {koeff[0]:>17.2e} | {R2:.4f}")
```

Da `zugversuch.csv` keine fehlenden Werte enthält, können wir hier auf
`.dropna()` verzichten.

Stahl hat die größte Steigung. Eine große Steigung in N/mm bedeutet, dass für
eine bestimmte Verlängerung eine hohe Kraft erforderlich ist. Der Werkstoff ist
also steifer. Stahl besitzt den höchsten E-Modul der drei Werkstoffe und
widersteht daher der Verformung am stärksten. Aluminium hat die kleinste
Steigung und ist unter denselben Bedingungen am nachgiebigsten.
````

````{admonition} Übung 11.5 (✩✩✩) Mini-Projekt: E-Modul-Bestimmung
:class: tip
Das Hookesche Gesetz verbindet Spannung $\sigma$ und Dehnung $\varepsilon$ über
den **E-Modul** $E$:

$$\sigma = E \cdot \varepsilon$$

Die Steigung einer Regressionsgeraden durch ein Spannungs-Dehnungs-Diagramm
entspricht direkt dem E-Modul. Ziel dieser Aufgabe ist es, den E-Modul aller
drei Werkstoffe experimentell aus den Messdaten zu bestimmen und mit den
Literaturwerten zu vergleichen.

Literaturwerte: Stahl 210 000 MPa, Aluminium 70 000 MPa, Titan 110 000 MPa.

**Teil 1: Kenngrößen berechnen**

Berechnen Sie die Spalten `Spannung_MPa` und `Dehnung_Proz` wie in Übung 11.2.

**Teil 2: E-Modul je Werkstoff**

Führen Sie für jeden Werkstoff eine lineare Regression von `Spannung_MPa`
gegen `Dehnung_Proz` durch. Die Steigung hat die Einheit MPa/%, daher gilt:

$$E = \text{Steigung} \cdot 100$$

Berechnen Sie außerdem R² und die relative Abweichung vom Literaturwert in
Prozent:

$$\text{Abweichung} = \frac{|E_{\text{berechnet}} - E_{\text{Literatur}}|}{E_{\text{Literatur}}} \cdot 100$$

**Teil 3: Ausgabe**

Geben Sie die Ergebnisse formatiert aus:

```
Werkstoff  | E_berechnet (MPa) | E_Literatur (MPa) | Abw. (%) | R²
-----------|-------------------|-------------------|----------|------
Stahl      |          ...      |        210000     |   ...    | ...
```

**Teil 4: Visualisierung**

Erstellen Sie ein Streudiagramm von `Dehnung_Proz` gegen `Spannung_MPa` mit
`color="Werkstoff"`. Zeichnen Sie für jeden Werkstoff eine Regressionsgerade
mit `fig.add_scatter()` ein.

Strukturieren Sie Ihren Code mit EVA-Kommentaren.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import pandas as pd
import numpy as np
import plotly.express as px

# Eingabe
df = pd.read_csv("zugversuch.csv")
L0_mm = 100.0
E_literatur = {"Stahl": 210000, "Aluminium": 70000, "Titan": 110000}

# Verarbeitung: neue Spalten
df["Spannung_MPa"] = df["Kraft_N"] / df["Querschnitt_mm2"]
df["Dehnung_Proz"] = (df["Verlaengerung_mm"] / L0_mm) * 100

# Ausgabe: Tabelle
print(f"{'Werkstoff':<12} | {'E_ber. (MPa)':>13} | "
      f"{'E_Lit. (MPa)':>13} | {'Abw. (%)':>9} | {'R²':>6}")
print("-" * 65)

ergebnisse = {}
for mat in ["Stahl", "Aluminium", "Titan"]:
    sub = df[df["Werkstoff"] == mat]
    x = sub["Dehnung_Proz"].values
    y = sub["Spannung_MPa"].values
    koeff = np.polyfit(x, y, 1)
    gerade = np.poly1d(koeff)
    R2 = np.corrcoef(x, y)[0, 1]**2
    E_ber = koeff[0] * 100
    abw = abs(E_ber - E_literatur[mat]) / E_literatur[mat] * 100
    ergebnisse[mat] = (koeff, gerade, R2)
    print(f"{mat:<12} | {E_ber:>13.0f} | "
          f"{E_literatur[mat]:>13d} | {abw:>9.2f} | {R2:.4f}")

# Ausgabe: Visualisierung
fig = px.scatter(data_frame=df,
                 x="Dehnung_Proz",
                 y="Spannung_MPa",
                 color="Werkstoff",
                 opacity=0.4,
                 title="Spannungs-Dehnungs-Diagramm mit Regressionsgeraden",
                 labels={"Dehnung_Proz": "Dehnung (%)",
                         "Spannung_MPa": "Spannung (MPa)"})

for mat, (koeff, gerade, R2) in ergebnisse.items():
    sub = df[df["Werkstoff"] == mat]
    x_fit = np.linspace(sub["Dehnung_Proz"].min(),
                        sub["Dehnung_Proz"].max(), 200)
    fig.add_scatter(x=x_fit,
                    y=gerade(x_fit),
                    mode="lines",
                    name=f"{mat} (Regression)")

fig.show()
```

Da `zugversuch.csv` keine fehlenden Werte enthält, können wir hier auf
`.dropna()` verzichten.

Ausgabe (Beispiel):
```
Werkstoff    | E_ber. (MPa)  | E_Lit. (MPa)  | Abw. (%)  |    R²
-----------------------------------------------------------------
Stahl        |        209942 |        210000 |      0.03 | 0.9979
Aluminium    |         70140 |         70000 |      0.20 | 0.9978
Titan        |        110343 |        110000 |      0.31 | 0.9980
```

Die berechneten E-Moduln weichen weniger als 0.4 % von den Literaturwerten ab.
Die hohen R²-Werte nahe 1.0 bestätigen, dass das Hookesche Gesetz den
elastischen Bereich sehr gut beschreibt. Im Spannungs-Dehnungs-Diagramm
liegen die drei Geraden klar getrennt: Stahl hat die steilste Kennlinie
(höchster E-Modul), Aluminium die flachste (niedrigster E-Modul). Das Diagramm
entspricht dem klassischen Spannungs-Dehnungs-Diagramm aus der
Werkstoffkunde, hier im elastischen Bereich.
````
