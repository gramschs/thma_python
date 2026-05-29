---
kernelspec:
  name: python3
  display_name: 'Python 3'
---

# 10.2 Filtern und Auswerten

In Kapitel 10.1 haben wir gelernt, einen DataFrame einzulesen, seine Struktur zu
erkunden und neue Spalten durch Vektoroperationen zu berechnen. In diesem Kapitel
werten wir den AutoScout24-Datensatz gezielt aus. Wir filtern Zeilen nach
bestimmten Bedingungen, vergleichen Fahrzeuggruppen miteinander und gehen mit
fehlenden Werten um. Der bereinigte DataFrame steht am Ende direkt für die
Visualisierung und Regression in Kapitel 11 bereit.

## Lernziele

```{admonition} Lernziele
:class: attention
* [ ] Sie können Zeilen eines DataFrames mit einer booleschen Maske filtern.
* [ ] Sie können mehrere Filterbedingungen mit `&` und `|` kombinieren.
* [ ] Sie können mit `.unique()` und `.value_counts()` die Kategorien einer
  Spalte erkunden.
* [ ] Sie können Gruppen manuell filtern und statistisch vergleichen.
* [ ] Sie können fehlende Werte mit `.isna()` aufspüren und mit `.dropna()`
  entfernen.
```

## Zeilen filtern mit booleschen Masken

In Kapitel 4 haben wir gelernt, Ausdrücke wie `preis > 20000` auszuwerten, die
einen booleschen Wert (`True` oder `False`) zurückgeben. Pandas überträgt dieses
Prinzip direkt auf ganze Spalten: Wendet man einen Vergleich auf eine Spalte an,
erhält man eine Series aus `True`- und `False`-Werten, eine sogenannte
**boolesche Maske**.

Wir laden zunächst wieder den Datensatz:

```{code-cell} python
import pandas as pd

df = pd.read_csv("autoscout24_DE_2020_cleaned.csv")
```

Als Beispiel erzeugen wir eine Maske für alle Elektrofahrzeuge:

```{code-cell} python
maske = df["Kraftstoff"] == "Elektro"
print(maske.head(10))
```

Die Maske enthält für jede Zeile `True`, wenn die Bedingung erfüllt ist, und
`False`, wenn nicht. Übergeben wir die Maske in eckigen Klammern an den
DataFrame, erhalten wir nur die Zeilen, für die `True` gilt:

```{code-cell} python
elektro = df[df["Kraftstoff"] == "Elektro"]
print(elektro.shape)
```

In der Praxis schreibt man die Maske direkt in die eckigen Klammern, ohne sie in
einer eigenen Variable zu speichern. Der DataFrame `elektro` enthält nur noch
die Elektrofahrzeuge und lässt sich genauso wie der ursprüngliche DataFrame
weiter auswerten.

### Bedingungen kombinieren

Mehrere Bedingungen lassen sich mit `&` (und) und `|` (oder) kombinieren. Das
entspricht `and` und `or` aus Kapitel 7, funktioniert in Pandas aber mit anderen
Operatoren. Außerdem muss jede einzelne Bedingung in Klammern stehen:

```{code-cell} python
# Elektrofahrzeuge mit einem Preis unter 25000 Euro
guenstige_elektro = df[(df["Kraftstoff"] == "Elektro") & (df["Preis (Euro)"] < 25000)]
print(guenstige_elektro.shape)
```

```{admonition} Klammerpflicht bei kombinierten Bedingungen
:class: warning
In Pandas müssen bei kombinierten Bedingungen beide Teile in runden Klammern
stehen. Ohne Klammern führt die Auswertungsreihenfolge zu einem Typfehler:

`df[df["Kraftstoff"] == "Elektro" & df["Preis (Euro)"] < 25000]`

Korrekt ist:

`df[(df["Kraftstoff"] == "Elektro") & (df["Preis (Euro)"] < 25000)]`

Der Grund liegt in der Operatorpriorität: `&` bindet stärker als `==`, was ohne
Klammern zu einer unerwarteten Auswertungsreihenfolge führt.
```

````{admonition} Mini-Übung
:class: tip
Filtern Sie den Datensatz nach Fahrzeugen mit Schaltgetriebe, die mehr als
150 kW Leistung haben. Wie viele Fahrzeuge erfüllen diese Bedingung? Geben Sie
außerdem den mittleren Preis dieser Fahrzeuge aus.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import pandas as pd

df = pd.read_csv("autoscout24_DE_2020_cleaned.csv")

# Filtern
stark_schalt = df[(df["Getriebe"] == "Schaltgetriebe") & (df["Leistung (kW)"] > 150)]

# Anzahl und mittlerer Preis
print(stark_schalt.shape[0])
print(stark_schalt["Preis (Euro)"].mean())
```

Die Ausgabe zeigt die Anzahl der Fahrzeuge, die beide Bedingungen gleichzeitig
erfüllen. Der Mittelwert liegt deutlich über dem Gesamtdurchschnitt des
Datensatzes, was plausibel ist: leistungsstarke Fahrzeuge mit Schaltgetriebe
sind häufig Sportwagen oder hochwertige Limousinen.
````

## Einfache Auswertung nach Gruppen

Bevor wir Gruppen vergleichen, verschaffen wir uns einen Überblick darüber,
welche Kategorien in einer Spalte überhaupt vorkommen. Die Methode `.unique()`
gibt alle eindeutigen Werte zurück:

```{code-cell} python
print(df["Kraftstoff"].unique())
```

Die Methode `.value_counts()` zählt zusätzlich, wie oft jeder Wert vorkommt, und
sortiert das Ergebnis absteigend:

```{code-cell} python
print(df["Kraftstoff"].value_counts())
```

Die Ausgabe zeigt, dass Benzin und Diesel mit Abstand am häufigsten vertreten
sind. Für einen Gruppenvergleich beschränken wir uns deshalb auf diese beiden
Kategorien.

Der direkte Weg zum Gruppenvergleich führt über das Filtern aus dem letzten
Abschnitt: Wir erzeugen für jede Gruppe einen eigenen DataFrame und berechnen
die gewünschten Kennzahlen separat.

```{code-cell} python
benzin = df[df["Kraftstoff"] == "Benzin"]
diesel = df[df["Kraftstoff"] == "Diesel"]

print(f"Benzin:  {benzin['Preis (Euro)'].mean():.0f} Euro (n = {len(benzin)})")
print(f"Diesel:  {diesel['Preis (Euro)'].mean():.0f} Euro (n = {len(diesel)})")
```

Neben dem Mittelwert ist die Standardabweichung eine wichtige Kennzahl, da sie
zeigt, wie stark die Preise innerhalb einer Gruppe streuen:

```{code-cell} python
print(f"Benzin Std:  {benzin['Preis (Euro)'].std():.0f} Euro")
print(f"Diesel Std:  {diesel['Preis (Euro)'].std():.0f} Euro")
```

````{admonition} Mini-Übung
:class: tip
Vergleichen Sie Fahrzeuge mit Automatikgetriebe und Fahrzeuge mit
Schaltgetriebe hinsichtlich ihrer mittleren Leistung in kW und ihres mittleren
Preises. Geben Sie für beide Gruppen jeweils Mittelwert und Standardabweichung
aus. Was beobachten Sie?
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import pandas as pd

df = pd.read_csv("autoscout24_DE_2020_cleaned.csv")

automatik    = df[df["Getriebe"] == "Automatik"]
schaltung    = df[df["Getriebe"] == "Schaltgetriebe"]

print("Leistung (kW):")
print(f"  Automatik:      {automatik['Leistung (kW)'].mean():.1f} kW  (Std: {automatik['Leistung (kW)'].std():.1f})")
print(f"  Schaltgetriebe: {schaltung['Leistung (kW)'].mean():.1f} kW  (Std: {schaltung['Leistung (kW)'].std():.1f})")

print("Preis (Euro):")
print(f"  Automatik:      {automatik['Preis (Euro)'].mean():.0f} Euro  (Std: {automatik['Preis (Euro)'].std():.0f})")
print(f"  Schaltgetriebe: {schaltung['Preis (Euro)'].mean():.0f} Euro  (Std: {schaltung['Preis (Euro)'].std():.0f})")
```

Fahrzeuge mit Automatikgetriebe haben im Datensatz im Mittel sowohl eine höhere
Leistung als auch einen höheren Preis als solche mit Schaltgetriebe. Das liegt
nicht nur am Getriebe selbst, sondern daran, dass Automatikgetriebe besonders
häufig in Fahrzeugen der Oberklasse verbaut werden, die bereits aus anderen
Gründen teurer und leistungsstärker sind.
````

## Fehlende Werte

Reale Datensätze enthalten fast immer fehlende Werte. In Pandas werden fehlende
Werte als `NaN` gespeichert (englisch: *Not a Number*). Sie entstehen
beispielsweise, wenn in einem Inserat eine Angabe fehlt oder beim Export aus
einer Datenbank kein Wert vorhanden war.

Mit `.isna()` erzeugen wir eine boolesche Maske, die für jede Zelle anzeigt, ob
ein Wert fehlt. `.isna().sum()` zählt die fehlenden Werte pro Spalte:

```{code-cell} python
print(df.isna().sum())
```

Im AutoScout24-Datensatz fehlen in der Spalte `Leistung (kW)` 14 Werte und in
der Spalte `Farbe` 20 Werte. Das sind etwa 0.1 Prozent aller Zeilen, was für
einen realen Datensatz sehr wenig ist.

Für viele Auswertungen müssen fehlende Werte entfernt werden, da sie
Berechnungen verfälschen oder Fehler verursachen können. Die Methode `.dropna()`
entfernt Zeilen mit fehlenden Werten. Mit dem Parameter `subset` schränken wir
das auf eine bestimmte Spalte ein, sodass nur Zeilen entfernt werden, in denen
genau diese Spalte fehlt:

```{code-cell} python
df_clean = df.dropna(subset=["Leistung (kW)"])
print(f"Vorher: {df.shape[0]} Zeilen")
print(f"Nachher: {df_clean.shape[0]} Zeilen")
```

Ohne `subset` würde `.dropna()` jede Zeile entfernen, in der irgendeine Spalte
einen fehlenden Wert enthält. Das wäre in den meisten Fällen zu aggressiv.

```{admonition} Wann entfernen, wann ersetzen?
:class: note
`.dropna()` entfernt die betroffenen Zeilen vollständig. Das ist sinnvoll, wenn
der fehlende Wert für die geplante Auswertung zwingend benötigt wird und die
Anzahl der betroffenen Zeilen klein ist. Fehlen hingegen sehr viele Werte, kann
das Entfernen den Datensatz verzerren. In solchen Fällen bietet Pandas die
Methode `.fillna()`, mit der fehlende Werte durch einen festen Wert oder den
Spaltenmittelwert ersetzt werden können.
```

````{admonition} Mini-Übung
:class: tip
1. Wie viele Zeilen enthalten in der Spalte `Farbe` einen fehlenden Wert?
2. Erstellen Sie einen bereinigten DataFrame `df_clean`, der weder in `Farbe`
   noch in `Leistung (kW)` fehlende Werte enthält. Verwenden Sie `.dropna()`
   mit dem Parameter `subset` und einer Liste beider Spaltennamen.
3. Vergleichen Sie `.shape` von `df` und `df_clean`.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import pandas as pd

df = pd.read_csv("autoscout24_DE_2020_cleaned.csv")

# 1. Fehlende Werte in Farbe
print(df["Farbe"].isna().sum())

# 2. Bereinigter DataFrame
df_clean = df.dropna(subset=["Farbe", "Leistung (kW)"])

# 3. Vergleich
print(f"Vorher: {df.shape}")
print(f"Nachher: {df_clean.shape}")
```

Da manche Fahrzeuginserate sowohl bei `Farbe` als auch bei `Leistung (kW)` einen
fehlenden Wert haben können, ist die Anzahl der entfernten Zeilen kleiner oder
gleich der Summe der einzelnen fehlenden Werte. `.dropna()` entfernt jede Zeile,
in der mindestens eine der angegebenen Spalten leer ist, aber zählt Zeilen mit
mehreren fehlenden Werten nur einmal.
````

## Zusammenfassung und Ausblick

In diesem Kapitel haben wir den AutoScout24-Datensatz gezielt ausgewertet.
Boolesche Masken ermöglichen es, Zeilen nach beliebigen Bedingungen zu filtern,
wobei kombinierte Bedingungen mit `&` und `|` und zwingenden Klammern formuliert
werden. Mit `.unique()` und `.value_counts()` lassen sich Kategorien erkunden,
und durch manuelles Filtern können Gruppen statistisch verglichen werden. Für
fehlende Werte bietet Pandas `.isna()` zur Diagnose und `.dropna()` zur
Bereinigung. Im nächsten Kapitel übergeben wir den bereinigten DataFrame direkt
an Plotly Express und führen eine lineare Regression durch.
