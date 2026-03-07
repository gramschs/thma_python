---
kernelspec:
  name: python3
  display_name: 'Python 3'
---

# 8.1 Funktionen selbst schreiben

Bisher haben wir viele fertige Funktionen benutzt: `print()`, `len()`,
`range()`, `px.line()` oder `np.random.normal()`. All diese Funktionen nehmen
Argumente entgegen, verarbeiten sie und liefern ein Ergebnis zurück. In diesem
Kapitel lernen wir, eigene Funktionen zu schreiben. Das lohnt sich immer dann,
wenn dieselbe Berechnung an mehreren Stellen im Programm gebraucht wird oder
wenn ein Code-Block einen klar abgrenzbaren Teilauftrag erfüllt.

Beispielsweise haben wir in Kapitel 5 den Bremsweg mit der Formel
$s_B = v^2 / 100$ immer wieder direkt im Code berechnet. Als eigene Funktion
formuliert, hat diese Berechnung einen Namen, kann mit einem Docstring
dokumentiert werden und ist sofort wiederverwendbar.

## Lernziele

```{admonition} Lernziele
:class: attention
* [ ] Sie kennen die Fachbegriffe **Aufruf**, **Argument**, **Parameter** und
  **Rückgabewert** einer Funktion und können sie korrekt verwenden.
* [ ] Sie können eine einfache Funktion mit `def` selbst implementieren und
  aufrufen.
* [ ] Sie können Funktionen mit Parametern und Rückgabewert (`return`)
  implementieren.
* [ ] Sie können eine Funktion mit einem **Docstring** dokumentieren.
```

## Einfache Funktionen ohne Parameter

Eine Funktion wird mit dem Schlüsselwort `def` definiert, gefolgt vom
Funktionsnamen und runden Klammern. Die Anweisungen im Inneren der Funktion
werden eingerückt. Die allgemeine Syntax lautet:

```python
def funktionsname():
    anweisung01
    anweisung02
    ...
```

Das folgende Beispiel zeigt eine Funktion, die eine Statusmeldung ausgibt:

```{code-cell} python
def zeige_status():
    print('System bereit.')
```

Wichtig: Die Definition führt die Funktion noch nicht aus. Sie legt lediglich
fest, was die Funktion tun soll, wenn sie aufgerufen wird. Der **Aufruf**
erfolgt anschließend durch den Funktionsnamen mit runden Klammern:

```{code-cell} python
zeige_status()
```

Und wie alle anderen Anweisungen kann auch ein Funktionsaufruf in einer
for-Schleife verwendet werden:

```{code-cell} python
for i in range(3):
    zeige_status()
```

## Funktionen mit Parametern

Meistens sollen Funktionen mit unterschiedlichen Eingaben arbeiten. Dafür werden
beim Definieren der Funktion **Parameter** eingeführt. So werden in der
Informatik die Variablennamen in den runden Klammern genannt, die beim Aufruf
durch konkrete Werte ersetzt werden:

```python
def funktionsname(parameter1, parameter2):
    anweisung01
    anweisung02
    ...
```

Als Beispiel erweitern wir die Statusmeldung um eine Bauteilbezeichnung:

```{code-cell} python
def zeige_status_bauteil(bezeichnung):
    print(f'Bauteil {bezeichnung}: System bereit.')
```

Beim Aufruf übergeben wir einen konkreten Wert als **Argument**. Der formale
Parameter `bezeichnung` nimmt dann den Wert dieses Arguments an:

```{code-cell} python
zeige_status_bauteil('Bremsscheibe')
zeige_status_bauteil('Lager')
```

```{admonition} Parameter vs. Argument
:class: caution
**Parameter** sind die Variablennamen in der Funktionsdefinition (z.B.
`bezeichnung` in `def zeige_status_bauteil(bezeichnung):`). Sie dienen als
Platzhalter. **Argumente** sind die konkreten Werte beim Aufruf (z.B.
`'Bremsscheibe'`). Der Unterschied ist ähnlich wie zwischen einer Formel mit
Variablen und einer Berechnung mit eingesetzten Zahlen.
```

## Funktionen mit Rückgabewert

Bisher haben unsere Funktionen nur Ausgaben auf dem Bildschirm erzeugt. In
der Regel soll das Ergebnis einer Berechnung jedoch für die weitere Verarbeitung
zur Verfügung stehen. Dafür gibt es das Schlüsselwort `return`:

```python
def funktionsname(parameter1, parameter2):
    anweisung01
    anweisung02
    ...
    return rueckgabewert
```

`return` beendet die Funktion sofort und übergibt den angegebenen Wert an die
aufrufende Stelle. Dieser **Rückgabewert** kann in einer Variablen gespeichert
oder direkt weiterverwendet werden.

Als Beispiel schreiben wir die Bremsweg-Formel aus Kapitel 5 als Funktion.
Die Formel lautet: $s_B = v^2 / 100$, wobei $v$ in km/h angegeben wird und
$s_B$ in Metern:

```{code-cell} python
def berechne_bremsweg(v_kmh):
    bremsweg_m = v_kmh**2 / 100
    return bremsweg_m
```

Jetzt können wir die Funktion aufrufen und das Ergebnis weiterverwenden:

```{code-cell} python
# Einzelberechnung
s = berechne_bremsweg(100)
print(f'Bremsweg bei 100 km/h: {s:.1f} m')
```

Der eigentliche Mehrwert zeigt sich, wenn die Funktion in einer Schleife
eingesetzt wird. Der Berechnungscode wird nicht wiederholt, sondern nur
einmal in der Funktion formuliert:

```{code-cell} python
for v in range(30, 131, 10):
    s = berechne_bremsweg(v)
    print(f'v = {v:3d} km/h,  Bremsweg = {s:5.1f} m')
```

```{admonition} Mini-Übung
:class: tip
Der Anhalteweg eines Fahrzeugs setzt sich aus Reaktionsweg und Bremsweg
zusammen: $s_{ges} = s_R + s_B = v / 3.6 + v^2 / 100$, wobei $v$ in km/h
angegeben wird und eine Reaktionszeit von 1 s angenommen wird.

Schreiben Sie eine Funktion `berechne_anhalteweg(v_kmh)`, die den gesamten
Anhalteweg in Metern zurückgibt. Verwenden Sie darin `berechne_bremsweg()`.

Rufen Sie anschließend die Funktion für 50, 80 und 100 km/h auf und geben Sie
die Ergebnisse mit f-String formatiert aus.
```

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
def berechne_anhalteweg(v_kmh):
    reaktionsweg_m = v_kmh / 3.6
    bremsweg_m = berechne_bremsweg(v_kmh)
    return reaktionsweg_m + bremsweg_m

for v in [50, 80, 100]:
    s = berechne_anhalteweg(v)
    print(f'v = {v:3d} km/h,  Anhalteweg = {s:5.1f} m')
```

Ausgabe:
```
v =  50 km/h,  Anhalteweg =  38.9 m
v =  80 km/h,  Anhalteweg =  86.2 m
v = 100 km/h,  Anhalteweg = 127.8 m
```
````

## Mehrere Rückgabewerte

Eine Python-Funktion kann mit `return` auch mehrere Werte gleichzeitig (in Form
eines sogenannten Tupels) zurückgeben, indem diese durch Kommas getrennt werden:

```python
def funktionsname(parameter):
    ...
    return wert1, wert2
```

Beim Aufruf weist man die Rückgabewerte durch Kommas getrennt mehreren
Variablen zu:

```{code-cell} python
def berechne_wege(v_kmh):
    reaktionsweg_m = v_kmh / 3.6
    bremsweg_m = v_kmh**2 / 100
    return reaktionsweg_m, bremsweg_m
```

```{code-cell} python
s_r, s_b = berechne_wege(100)
print(f'Reaktionsweg: {s_r:.1f} m')
print(f'Bremsweg:     {s_b:.1f} m')
```

## Funktionen dokumentieren: der Docstring

Eine gute Funktion erklärt sich durch ihren Namen und ihre Parameter. Darüber
hinaus ist es Konvention, direkt nach der `def`-Zeile einen kurzen
Beschreibungstext in dreifache Anführungszeichen zu schreiben, den sogenannten
**Docstring**:

```{code-cell} python
def berechne_bremsweg(v_kmh):
    """Berechnet den Bremsweg in Metern für eine gegebene Geschwindigkeit in km/h."""
    bremsweg_m = v_kmh**2 / 100
    return bremsweg_m
```

Python liest den Docstring automatisch aus und stellt ihn über `help()` zur
Verfügung, genauso wie bei den eingebauten Funktionen:

```{code-cell} python
help(berechne_bremsweg)
```

```{admonition} Mini-Übung
:class: tip
Schreiben Sie eine Funktion `berechne_leistung(U_V, I_A)`, die die elektrische
Leistung nach $P = U \cdot I$ berechnet und in Watt zurückgibt. Versehen Sie
die Funktion mit einem Docstring.

Testen Sie die Funktion für folgende Werte und geben Sie die Ergebnisse
formatiert aus:

| Spannung $U$ | Strom $I$ | erwartete Leistung $P$ |
|-------------|-----------|----------------------|
| 230 V | 10 A | 2300 W |
| 12 V | 5 A | 60 W |
| 400 V | 16 A | 6400 W |
```

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
def berechne_leistung(U_V, I_A):
    """Berechnet die elektrische Leistung P = U * I in Watt."""
    return U_V * I_A

# Test
messwerte = [(230, 10), (12, 5), (400, 16)]

for U, I in messwerte:
    P = berechne_leistung(U, I)
    print(f'U = {U:3d} V,  I = {I:2d} A,  P = {P:4.0f} W')
```

Ausgabe:
```
U = 230 V,  I = 10 A,  P = 2300 W
U =  12 V,  I =  5 A,  P =   60 W
U = 400 V,  I = 16 A,  P = 6400 W
```
````

```{dropdown} Video "Funktionen" von Programmieren Starten
<iframe width="560" height="315" src="https://www.youtube.com/embed/LQCfN5HS9xI"
title="YouTube video player" frameborder="0" allow="accelerometer; autoplay;
clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
allowfullscreen></iframe>
```

## Zusammenfassung und Ausblick

In diesem Kapitel haben wir gelernt, eigene Funktionen mit `def` zu
implementieren. Eine Funktion fasst Anweisungen unter einem Namen zusammen und
kann mit Parametern flexibel gestaltet werden. Mit `return` gibt sie Ergebnisse
zurück, die an der aufrufenden Stelle weiterverwendet werden können. Mehrere
Rückgabewerte sind durch Komma möglich. Ein Docstring dokumentiert die Funktion
so, dass `help()` eine Beschreibung ausgibt. Im nächsten Kapitel wenden wir
Funktionen auf physikalische Formeln an und kombinieren sie mit Schleifen und
Plotly Express, um Kennlinien zu visualisieren.
