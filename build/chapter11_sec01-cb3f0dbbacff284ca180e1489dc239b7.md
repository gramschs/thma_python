---
kernelspec:
  name: python3
  display_name: 'Python 3'
---

# 11.1 Visualisierung mit DataFrames

In den Kapiteln 3 bis 9 haben wir Plotly Express stets mit Listen oder
NumPy-Arrays gefüttert: Wir haben Spalten mühsam extrahiert, in Variablen
gespeichert und dann einzeln übergeben. Seit Kapitel 10 arbeiten wir mit
DataFrames. Plotly Express kann einen DataFrame direkt entgegennehmen, wir
übergeben dann nur noch Spaltennamen als Strings. Das macht den Code kürzer,
die Achsenbeschriftungen vollständiger und ermöglicht eine automatische
Einfärbung nach Kategorien mit einem einzigen Parameter. In diesem Kapitel
lernen wir drei Diagrammtypen mit dieser neuen Syntax kennen.

## Lernziele

```{admonition} Lernziele
:class: attention
* [ ] Sie können `px.scatter()` mit `data_frame=`, `x=`, `y=` und `color=`
  aufrufen und kennen den Vorteil gegenüber der Listen-Syntax.
* [ ] Sie können mit `px.box()` einen **Boxplot** erstellen und die Elemente
  Median, Quartile und Ausreißer ablesen.
* [ ] Sie können mit `px.histogram()` und `color=` zwei Verteilungen in einem
  Diagramm vergleichen.
```

## Streudiagramm mit DataFrame und `color=`

Wir laden zunächst den bereinigten AutoScout24-Datensatz aus Kapitel 10 und
filtern ihn bezüglich der vier häufigsten Kraftstoffarten sowie bezüglich der
Preise bis 150.000 Euro, um Ausreißer in der Visualisierung zu vermeiden:

```{code-cell} python
import pandas as pd
import plotly.express as px

# Eingabe
df = pd.read_csv("autoscout24_DE_2020_cleaned.csv")

haupttypen = ["Benzin", "Diesel", "Hybrid", "Elektro"]
df_plot = df[(df["Kraftstoff"].isin(haupttypen)) &
             (df["Preis (Euro)"] <= 150000)]
```

`df["Kraftstoff"].isin(haupttypen)` prüft für jede Zeile, ob der Eintrag in der
Spalte Kraftstoff in der Liste `haupttypen` enthalten ist. Das Ergebnis ist eine
Boolesche Spalte aus True/False-Werten, die wir  zur Zeilenauswahl verwenden.

Bisher haben wir Plotly Express immer so aufgerufen:

```python
px.scatter(x=df["Leistung (kW)"], y=df["Preis (Euro)"])
```

Mit dem Parameter `data_frame=` übergeben wir den gesamten DataFrame und
benennen die Spalten für die Achsen als Strings:

```{code-cell} python
# Ausgabe
fig = px.scatter(data_frame=df_plot,
                 x="Leistung (kW)",
                 y="Preis (Euro)",
                 title="Preis in Abhängigkeit der Leistung")
fig.show()
```

Der entscheidende Vorteil zeigt sich beim Parameter `color=`: Er färbt jeden
Punkt automatisch nach einer Spalte ein. Bei kategorialen Spalten entstehen
unterschiedliche Farben je Kategorie, bei numerischen Splten eine Farbskala.

```{code-cell} python
# Ausgabe
fig = px.scatter(data_frame=df_plot,
                 x="Leistung (kW)",
                 y="Preis (Euro)",
                 color="Kraftstoff",
                 title="Preis in Abhängigkeit der Leistung nach Kraftstoffart")
fig.show()
```

Die Spaltennamen erscheinen automatisch als Achsenbeschriftungen. Möchte man
sie anpassen, übergibt man dem Parameter `labels=` einen Ausdruck, der
Spaltennamen auf gewünschte Bezeichnungen abbildet:

```{code-cell} python
fig = px.scatter(data_frame=df_plot,
                 x="Leistung (kW)",
                 y="Preis (Euro)",
                 color="Kraftstoff",
                 labels={"Leistung (kW)": "Leistung in kW",
                         "Preis (Euro)": "Preis in Euro"},
                 title="Preis in Abhängigkeit der Leistung nach Kraftstoffart")
fig.show()
```

````{admonition} Mini-Übung
:class: tip
Erstellen Sie ein Streudiagramm mit `Kilometerstand (km)` auf der x-Achse und
`Preis (Euro)` auf der y-Achse. Färben Sie die Punkte nach `Getriebe` ein.
Beschränken Sie sich auf die Getriebearten `"Automatik"` und
`"Schaltgetriebe"`. Was beobachten Sie?
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
df = pd.read_csv("autoscout24_DE_2020_cleaned.csv")
df_getriebe = df[df["Getriebe"].isin(["Automatik", "Schaltgetriebe"])]

# Ausgabe
fig = px.scatter(data_frame=df_getriebe,
                 x="Kilometerstand (km)",
                 y="Preis (Euro)",
                 color="Getriebe",
                 title="Preis in Abhängigkeit des Kilometerstands nach Getriebeart")
fig.show()
```

Das Diagramm zeigt einen deutlich erkennbaren negativen Zusammenhang: Mit
steigendem Kilometerstand sinkt der Preis. Fahrzeuge mit Automatikgetriebe
sind bei gleichem Kilometerstand im Mittel teurer als solche mit
Schaltgetriebe.
````

## Boxplot für Gruppenvergleiche

Ein Streudiagramm zeigt jeden Datenpunkt einzeln, was bei fast 18.000 Punkten
schnell unübersichtlich wird. Der **Boxplot** fasst eine Verteilung in fünf
Kennzahlen zusammen und eignet sich daher besonders gut für Gruppenvergleiche.

```{admonition} Wie wird ein Boxplot interpretiert?
:class: note
Ein Boxplot besteht aus folgenden Elementen:

* Die **Box** reicht vom 25%-Quartil (Q1) bis zum 75%-Quartil (Q3) und enthält
  die mittleren 50 % aller Werte. Der Interquartilsabstand (IQR) ist der
  numerische Abstand zwischen Q3 und Q1, d.h. Q3 − Q1, und entspricht der Höhe
  der Box auf der Datenachse.
* Der **Strich in der Box** markiert den **Median**, also den mittleren Wert.
* Die **Whisker** (Antennen) erstrecken sich bis zum kleinsten bzw. größten
  Datenpunkt, der noch innerhalb des 1.5-fachen IGR unterhalb von Q1 bzw.
  oberhalb von Q3 liegt.
* Punkte außerhalb der Whisker sind **Ausreißer**.
```

Mit `px.box()` erstellen wir einen Boxplot. Wir übergeben die kategoriale
Spalte an `x=` und die numerische Spalte an `y=`:

```{code-cell} python
import pandas as pd
import plotly.express as px

# Eingabe
df = pd.read_csv("autoscout24_DE_2020_cleaned.csv")
df_getriebe = df[df["Getriebe"].isin(["Automatik", "Schaltgetriebe"])]

# Ausgabe
fig = px.box(data_frame=df_getriebe,
             x="Getriebe",
             y="Preis (Euro)",
             title="Preisverteilung nach Getriebeart")
fig.show()
```

Der Boxplot zeigt auf einen Blick, dass Fahrzeuge mit Automatikgetriebe nicht
nur im Median teurer sind, sondern auch stärker streuen. Das Streudiagramm aus
dem letzten Abschnitt hat denselben Befund gezeigt, aber der Boxplot kommuniziert
ihn kompakter.

Auch `px.box()` unterstützt den `color=`-Parameter. Das ist besonders nützlich,
wenn man eine zweite kategoriale Variable einbringen möchte:

```{code-cell} python
haupttypen = ["Benzin", "Diesel", "Hybrid", "Elektro"]
df_beide = df[(df["Getriebe"].isin(["Automatik", "Schaltgetriebe"])) &
              (df["Kraftstoff"].isin(haupttypen))]

fig = px.box(data_frame=df_beide,
             x="Getriebe",
             y="Preis (Euro)",
             color="Kraftstoff",
             title="Preisverteilung nach Getriebeart und Kraftstoff")
fig.show()
```

```{admonition} Mini-Übung
:class: tip
Erstellen Sie einen Boxplot, der die Verteilung der Leistung (`Leistung (kW)`)
für die vier Kraftstoffarten `"Benzin"`, `"Diesel"`, `"Hybrid"` und `"Elektro"`
vergleicht. Übergeben Sie `Kraftstoff` an `x=` und `Leistung (kW)` an `y=`.
Welche Kraftstoffart zeigt die größte Streuung?
```

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
df = pd.read_csv("autoscout24_DE_2020_cleaned.csv")
haupttypen = ["Benzin", "Diesel", "Hybrid", "Elektro"]
df_haupt = df[df["Kraftstoff"].isin(haupttypen)]

# Ausgabe
fig = px.box(data_frame=df_haupt,
             x="Kraftstoff",
             y="Leistung (kW)",
             title="Leistungsverteilung nach Kraftstoffart")
fig.show()
```

Die Benzinfahrzeuge zeigen den größten Interquartilsabstand und die meisten
Ausreißer nach oben, was die große Bandbreite von kleinen Stadtautos bis zu
Hochleistungsfahrzeugen widerspiegelt. Elektrofahrzeuge haben eine vergleichsweise
kompakte Verteilung.
````

## Histogramm mit `color=`

Das Histogramm kennen wir seit Kapitel 6. Damals haben wir eine Liste von
Zufallswerten übergeben. Mit `data_frame=` und `color=` lassen sich jetzt zwei
Verteilungen in einem einzigen Diagramm vergleichen.

Als Beispiel vergleichen wir die Kilometerstand-Verteilung von Fahrzeugen mit
Automatik- und Schaltgetriebe:

```{code-cell} python
import pandas as pd
import plotly.express as px

# Eingabe
df = pd.read_csv("autoscout24_DE_2020_cleaned.csv")
df_getriebe = df[df["Getriebe"].isin(["Automatik", "Schaltgetriebe"])]

# Ausgabe
fig = px.histogram(data_frame=df_getriebe,
                   x="Kilometerstand (km)",
                   color="Getriebe",
                   title="Kilometerstand-Verteilung nach Getriebeart")
fig.show()
```

Standardmäßig werden die Balken übereinander dargestellt (gestapelt). Für einen
Vergleich der Formen beider Verteilungen ist `barmode="overlay"` besser
geeignet. Der Parameter `opacity=` steuert die Deckkraft, damit beide Kurven
sichtbar bleiben:

```{code-cell} python
fig = px.histogram(data_frame=df_getriebe,
                   x="Kilometerstand (km)",
                   color="Getriebe",
                   barmode="overlay",
                   opacity=0.7,
                   title="Kilometerstand-Verteilung nach Getriebeart")
fig.show()
```

```{admonition} Was bewirkt der barmode?
:class: note
`barmode="overlay"` legt beide Histogramme übereinander, was den Formvergleich
erleichtert. `barmode="group"` stellt die Balken nebeneinander, was absolute
Häufigkeiten besser vergleichbar macht. Für Verteilungsvergleiche ist
`"overlay"` mit reduzierter Deckkraft meist die bessere Wahl.
```

````{admonition} Mini-Übung
:class: tip
Vergleichen Sie die Preisverteilung von Benzin- und Dieselfahrzeugen als
überlagertes Histogramm. Filtern Sie vorher Preise über 100.000 Euro heraus,
damit der relevante Bereich besser sichtbar wird. Verwenden Sie
`barmode="overlay"` und `opacity=0.7`.
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
df = pd.read_csv("autoscout24_DE_2020_cleaned.csv")
df_bd = df[(df["Kraftstoff"].isin(["Benzin", "Diesel"])) &
           (df["Preis (Euro)"] <= 100000)]

# Ausgabe
fig = px.histogram(data_frame=df_bd,
                   x="Preis (Euro)",
                   color="Kraftstoff",
                   barmode="overlay",
                   opacity=0.7,
                   title="Preisverteilung: Benzin vs. Diesel")
fig.show()
```

Beide Verteilungen sind rechtsschief: Die meisten Fahrzeuge kosten weniger als
40.000 Euro, nach oben gibt es aber einen langen Ausläufer. Die Verteilungen
überlappen stark, Dieselfahrzeuge sind im Mittel leicht teurer.
````

## Zusammenfassung und Ausblick

In diesem Kapitel haben wir Plotly Express mit DataFrames eingesetzt. Der
Parameter `data_frame=` ersetzt das manuelle Extrahieren von Spalten, und
`color=` färbt Punkte oder Balken automatisch nach einer Kategorie ein. Mit
`px.box()` haben wir einen neuen Diagrammtyp kennengelernt, der Verteilungen
kompakt zusammenfasst und besonders gut für Gruppenvergleiche geeignet ist. Das
Histogramm aus Kapitel 6 haben wir mit `barmode="overlay"` für den
Verteilungsvergleich erweitert. Im nächsten Kapitel berechnen wir eine lineare
Regressionsgerade und zeichnen sie in ein Streudiagramm ein.
