---
kernelspec:
  name: python3
  display_name: 'Python 3'
---

# Übungen

````{admonition} Übung 9.1 (✩)
:class: tip
Gegeben ist folgender Code:

```python
import numpy as np

a = [1, 2, 3] + [4, 5, 6]
b = np.array([1, 2, 3]) + np.array([4, 5, 6])
c = np.array([1, 2.0, 3])
d = np.array([10, 20, 30, 40, 50])
```

1. Sagen Sie vorher, was `print(a)` und `print(b)` ausgeben. Worin besteht
   der Unterschied?
2. Sagen Sie vorher, was `print(c.dtype)` ausgibt. Warum wählt NumPy diesen
   Typ, obwohl zwei der drei Werte ganze Zahlen sind?
3. Was geben `print(d[-1])` und `print(d[-2])` aus? Erklären Sie, warum der
   negative Index auch bei NumPy-Arrays funktioniert.
4. Führen Sie den Code aus und überprüfen Sie Ihre Vorhersagen.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import numpy as np

a = [1, 2, 3] + [4, 5, 6]
b = np.array([1, 2, 3]) + np.array([4, 5, 6])
c = np.array([1, 2.0, 3])
d = np.array([10, 20, 30, 40, 50])

print(a)         # [1, 2, 3, 4, 5, 6]
print(b)         # [5 7 9]
print(c.dtype)   # float64
print(d[-1])     # 50
print(d[-2])     # 40
```

Erklärung:
1. Bei Python-Listen bewirkt `+` eine Verkettung: Die beiden Listen werden zu
   einer zusammengefügt. Bei NumPy-Arrays bedeutet `+` eine elementweise
   Addition: Jedes Element des ersten Arrays wird zum entsprechenden Element
   des zweiten Arrays addiert.
2. NumPy wählt `float64`, weil das Array den Wert `2.0` enthält, der bereits
   ein Float ist. NumPy wandelt dann alle anderen Werte in denselben Typ um,
   da ein Array nur einen einzigen Datentyp enthalten kann. `int` kann
   verlustfrei in `float` umgewandelt werden, umgekehrt aber nicht.
3. `d[-1]` liefert `50` (letztes Element) und `d[-2]` liefert `40`
   (vorletztes Element). NumPy-Arrays unterstützen denselben negativen Index
   wie Python-Listen: Python berechnet intern den positiven Index, indem es
   die Länge des Arrays zum negativen Index addiert.
````

````{admonition} Übung 9.2 (✩)
:class: tip
Die Tagestemperatur lässt sich näherungsweise als Sinusfunktion modellieren.
Die Formel lautet:

$$T(t) = T_{avg} + A \cdot \sin\left(\frac{2\pi}{24} \cdot (t - t_{max})\right)$$

Dabei ist $t$ die Uhrzeit in Stunden (0 bis 24), $T_{avg}$ die mittlere
Tagestemperatur, $A$ die Amplitude und $t_{max}$ der Zeitpunkt der höchsten
Temperatur (typischerweise 14 Uhr).

Verwenden Sie folgende Werte: $T_{avg} = 22.0$ °C, $A = 6.0$ °C,
$t_{max} = 14.0$ h.

1. Erzeugen Sie eine Zeitachse von 0 bis 24 Stunden mit 500 Punkten und
   berechnen Sie den Temperaturverlauf als NumPy-Array.
2. Geben Sie die Temperatur um Mitternacht (letzter Wert des Arrays) mit
   einem negativen Index und f-String formatiert auf 1 Nachkommastelle aus.
3. Die maximale Tagestemperatur berechnet sich als $T_{avg} + A$. Prüfen Sie
   mit einer `if`-Bedingung, ob dieser Wert über 35 °C liegt, und geben Sie
   in diesem Fall `"Hitzewarnung!"` aus.

Strukturieren Sie Ihren Code mit EVA-Kommentaren.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import numpy as np
import plotly.express as px

# Eingabe
T_avg   = 22.0   # mittlere Temperatur in °C
A       = 6.0    # Amplitude in °C
t_max   = 14.0   # Uhrzeit des Maximums in h

# Verarbeitung
t     = np.linspace(0, 24, 500)
T     = T_avg + A * np.sin(2 * np.pi / 24 * (t - t_max))
T_max = T_avg + A

# Ausgabe
print(f"Temperatur um Mitternacht: {T[-1]:.1f} °C")

if T_max > 35.0:
    print("Hitzewarnung!")
```

Ausgabe:
```
Temperatur um Mitternacht: 18.0 °C
```

Die Hitzewarnung wird nicht ausgegeben, da die maximale Temperatur
$22.0 + 6.0 = 28.0$ °C beträgt.
````

````{admonition} Übung 9.3 (✩✩)
:class: tip
Das Kapitalwachstum bei kontinuierlicher Verzinsung folgt der
Exponentialfunktion:

$$K(t) = K_0 \cdot e^{r \cdot t}$$

Dabei ist $K_0$ das Startkapital in Euro, $r$ der jährliche Zinssatz (als
Dezimalzahl, z. B. 0.03 für 3 %) und $t$ die Zeit in Jahren.

1. Schreiben Sie eine Funktion `berechne_kapital(K0_euro, r, t)`, die das
   Kapital zum Zeitpunkt $t$ zurückgibt. Der Parameter `t` kann eine einzelne
   Zahl oder ein NumPy-Array sein. Versehen Sie die Funktion mit einem
   Docstring.
2. Berechnen Sie das Kapitalwachstum für ein Startkapital von 10.000 € über
   30 Jahre für folgende zwei Szenarien und erstellen Sie für jedes Szenario
   ein eigenes Liniendiagramm:

   | Szenario | Zinssatz |
   |----------|----------|
   | Normalzins | 3 % |
   | Hochzins | 6 % |

3. Das Zielkapital beträgt 25.000 €. Prüfen Sie für jedes Szenario mit einer
   `if/else`-Bedingung, ob das Zielkapital nach 30 Jahren erreicht wird, und
   geben Sie das Ergebnis formatiert aus. Verwenden Sie den negativen Index
   `K[-1]`, um das Endkapital abzulesen.

Strukturieren Sie Ihren Code mit EVA-Kommentaren.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import numpy as np
import plotly.express as px

def berechne_kapital(K0_euro, r, t):
    """Berechnet das Kapital bei kontinuierlicher Verzinsung: K = K0 * e^(r*t).

    K0_euro: Startkapital in Euro
    r:       jährlicher Zinssatz als Dezimalzahl (z. B. 0.03 für 3 %)
    t:       Zeit in Jahren (Zahl oder NumPy-Array)
    """
    return K0_euro * np.exp(r * t)

# Eingabe
K0        = 10000.0   # Startkapital in Euro
ZIEL      = 25000.0   # Zielkapital in Euro
t         = np.linspace(0, 30, 500)

# Verarbeitung und Ausgabe: Normalzins
K2 = berechne_kapital(K0, 0.03, t)
fig2 = px.line(x=t, y=K2,
               labels={"x": "Jahre", "y": "Kapital (€)"},
               title="Kapitalwachstum bei 3 % Zinsen")
fig2.show()
if K2[-1] >= ZIEL:
    print(f"Normalzins: Ziel erreicht. Endkapital: {K2[-1]:.2f} Euro")
else:
    print(f"Normalzins: Ziel nicht erreicht. Endkapital: {K2[-1]:.2f} Euro")

# Verarbeitung und Ausgabe: Hochzins
K3 = berechne_kapital(K0, 0.06, t)
fig3 = px.line(x=t, y=K3,
               labels={"x": "Jahre", "y": "Kapital (€)"},
               title="Kapitalwachstum bei 6 % Zinsen")
fig3.show()
if K3[-1] >= ZIEL:
    print(f"Hochzins: Ziel erreicht. Endkapital: {K3[-1]:.2f} Euro")
else:
    print(f"Hochzins: Ziel nicht erreicht. Endkapital: {K3[-1]:.2f} Euro")
```

Ausgabe:
```
Normalzins: Ziel nicht erreicht. Endkapital: 24596.03 Euro
Hochzins: Ziel erreicht. Endkapital: 60496.47 Euro
```

Der Normalzins verfehlt das Ziel knapp, der Hochzins übertrifft es bei weitem.
Der Vergleich zeigt eindrücklich, wie stark der Zinssatz das Langzeitergebnis
beeinflusst: Zwei Prozentpunkte Unterschied bedeuten nach 30 Jahren fast das
Dreifache an Endkapital.
````

````{admonition} Übung 9.4 (✩✩)
:class: tip
Ein Fitness-Tracker zeichnet für eine Woche folgende tägliche Schrittzahlen
auf:

```python
schritte = np.array([6200, 11500, 4800, 9300, 7100, 12400, 3900])
wochentage = ["Mo", "Di", "Mi", "Do", "Fr", "Sa", "So"]
```

1. Berechnen Sie mit einer `for`-Schleife und einem Akkumulator die
   kumulierten Schritte am Ende jedes Tages (Montag: 6200, Dienstag: 17700,
   usw.) und speichern Sie die Werte in einer Liste.
2. Durchlaufen Sie die Schrittzahlen mit einer `for`-Schleife und
   klassifizieren Sie jeden Tag mit `elif`:
   - unter 5.000 Schritte: `"zu wenig"`
   - 5.000 bis unter 10.000 Schritte: `"ausreichend"`
   - 10.000 Schritte und mehr: `"sehr aktiv"`
   Geben Sie für jeden Tag den Wochentag, die Schrittzahl und die
   Klassifikation aus. Verwenden Sie eine Zählvariable, um auf den passenden
   Wochentag zuzugreifen.
3. Visualisieren Sie die täglichen Schrittzahlen als Balkendiagramm.

Strukturieren Sie Ihren Code mit EVA-Kommentaren.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import numpy as np
import plotly.express as px

# Eingabe
schritte   = np.array([6200, 11500, 4800, 9300, 7100, 12400, 3900])
wochentage = ["Mo", "Di", "Mi", "Do", "Fr", "Sa", "So"]

# Verarbeitung: kumulierte Schritte
kumuliert = []
summe = 0
for s in schritte:
    summe = summe + s
    kumuliert.append(summe)

# Verarbeitung und Ausgabe: Klassifikation
i = 0
for s in schritte:
    if s < 5000:
        klasse = "zu wenig"
    elif s < 10000:
        klasse = "ausreichend"
    else:
        klasse = "sehr aktiv"
    print(f"{wochentage[i]}: {s} Schritte ({klasse})")
    i = i + 1

print(f"Gesamtschritte: {kumuliert[-1]}")

# Ausgabe: Balkendiagramm
fig = px.bar(x=wochentage, y=schritte,
             labels={"x": "Wochentag", "y": "Schritte"},
             title="Tägliche Schrittzahlen")
fig.show()
```

Ausgabe:
```
Mo: 6200 Schritte (ausreichend)
Di: 11500 Schritte (sehr aktiv)
Mi: 4800 Schritte (zu wenig)
Do: 9300 Schritte (ausreichend)
Fr: 7100 Schritte (ausreichend)
Sa: 12400 Schritte (sehr aktiv)
So: 3900 Schritte (zu wenig)
Gesamtschritte: 55200
```

Die Schleife verwendet eine Zählvariable `i`, die zu Beginn auf 0 gesetzt
und am Ende jedes Durchgangs um 1 erhöht wird. So kann mit `wochentage[i]`
auf den zum aktuellen Schrittwert passenden Wochentag zugegriffen werden.
Das kumulierte Gesamt wird mit `kumuliert[-1]` abgelesen, da der letzte Wert
der Liste die Gesamtsumme enthält.
````

````{admonition} Übung 9.5 (✩✩)
:class: tip
Bei realen Messungen ist ein sauberes Signal immer von Rauschen überlagert.
In dieser Aufgabe simulieren wir ein verrauschtes Sinussignal.

Das saubere Signal lautet: $y(t) = \sin(2\pi \cdot 3 \cdot t)$ mit $t$ von
0 bis 1 Sekunde (500 Punkte). Das Rauschen ist normalverteilt mit Mittelwert
0 und Standardabweichung 0.15 (verwenden Sie `np.random.normal(0, 0.15, ...)`,
wobei der dritte Parameter die Anzahl der Punkte angibt, die sich aus
`t.shape[0]` ergibt).

1. Berechnen Sie das saubere Signal `y_sauber` und das verrauschte Signal
   `y_verrauscht = y_sauber + rauschen`.
2. Stellen Sie beide Signale in separaten Liniendiagrammen dar.
3. Berechnen Sie die Abweichung `abweichung = y_verrauscht - y_sauber`.
   Bestimmen Sie die maximale absolute Abweichung mit
   `max_abw = np.max(np.abs(abweichung))`. `np.abs()` berechnet dabei den
   Betrag jedes Elements, `np.max()` gibt den größten Wert des Arrays zurück.
4. Geben Sie die maximale Abweichung mit einem f-String formatiert auf
   2 Nachkommastellen aus.

Strukturieren Sie Ihren Code mit EVA-Kommentaren.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import numpy as np
import plotly.express as px

# Eingabe
t         = np.linspace(0, 1, 500)
rauschen  = np.random.normal(0, 0.15, len(t))

# Verarbeitung
y_sauber     = np.sin(2 * np.pi * 3 * t)
y_verrauscht = y_sauber + rauschen
abweichung   = y_verrauscht - y_sauber
max_abw      = np.max(np.abs(abweichung))

# Ausgabe
fig1 = px.line(x=t, y=y_sauber,
               labels={"x": "Zeit (s)", "y": "Amplitude"},
               title="Sauberes Signal")
fig1.show()

fig2 = px.line(x=t, y=y_verrauscht,
               labels={"x": "Zeit (s)", "y": "Amplitude"},
               title="Verrauschtes Signal")
fig2.show()

print(f"Maximale Abweichung: {max_abw:.2f}")
```

Die maximale Abweichung entspricht in etwa der dreifachen Standardabweichung
des Rauschens (ca. 0.45), was dem statistischen Erwartungswert für
normalverteiltes Rauschen entspricht. Da `np.random.normal()` zufällige Werte
erzeugt, variiert das Ergebnis bei jedem Durchlauf leicht. `np.abs()` berechnet
elementweise den Betrag des Abweichungs-Arrays, `np.max()` gibt daraus den
größten Wert zurück. Das ersetzt die manuelle Schleife durch einen einzigen
kompakten Ausdruck.
````

````{admonition} Übung 9.6 (✩✩)
:class: tip
Im freien Fall gilt ohne Luftwiderstand:

$$s(t) = \frac{1}{2} \cdot g \cdot t^2 \qquad v(t) = g \cdot t$$

Die Erdbeschleunigung $g$ ist auf verschiedenen Himmelskörpern unterschiedlich.

1. Schreiben Sie eine Funktion `berechne_fallhoehe(g, t)`, die die Fallhöhe
   in Metern zurückgibt. `t` ist ein NumPy-Array. Versehen Sie die Funktion
   mit einem Docstring.
2. Schreiben Sie eine Funktion `klassifiziere_planet(g)`, die anhand der
   Erdbeschleunigung eine Zeichenkette zurückgibt:
   - kleiner als 5 m/s²: `"leichter als die Erde"`
   - zwischen 5 und 15 m/s²: `"ähnlich wie die Erde"`
   - größer als 15 m/s²: `"schwerer als die Erde"`
3. Berechnen Sie die Fallhöhe für folgende drei Himmelskörper über 10 Sekunden
   und erstellen Sie für jeden ein eigenes Liniendiagramm. Fügen Sie die
   Klassifikation aus Aufgabe 2 in den Diagrammtitel ein.

   | Himmelskörper | Erdbeschleunigung |
   |---------------|-------------------|
   | Mond | 1.62 m/s² |
   | Erde | 9.81 m/s² |
   | Jupiter | 24.79 m/s² |

Strukturieren Sie Ihren Code mit EVA-Kommentaren.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import numpy as np
import plotly.express as px

def berechne_fallhoehe(g, t):
    """Berechnet die Fallhöhe im freien Fall ohne Luftwiderstand in Metern.

    g: Erdbeschleunigung in m/s²
    t: Zeitachse als NumPy-Array in s
    """
    return 0.5 * g * t**2

def klassifiziere_planet(g):
    """Klassifiziert einen Himmelskörper anhand seiner Erdbeschleunigung."""
    if g < 5.0:
        return "leichter als die Erde"
    elif g <= 15.0:
        return "ähnlich wie die Erde"
    else:
        return "schwerer als die Erde"

# Eingabe
t = np.linspace(0, 10, 500)

# Verarbeitung und Ausgabe: Mond
g_mond = 1.62
s_mond = berechne_fallhoehe(g_mond, t)
klasse_mond = klassifiziere_planet(g_mond)
fig1 = px.line(x=t, y=s_mond,
               labels={"x": "Zeit (s)", "y": "Fallhöhe (m)"},
               title=f"Freier Fall auf dem Mond (g = {g_mond} m/s², {klasse_mond})")
fig1.show()

# Verarbeitung und Ausgabe: Erde
g_erde = 9.81
s_erde = berechne_fallhoehe(g_erde, t)
klasse_erde = klassifiziere_planet(g_erde)
fig2 = px.line(x=t, y=s_erde,
               labels={"x": "Zeit (s)", "y": "Fallhöhe (m)"},
               title=f"Freier Fall auf der Erde (g = {g_erde} m/s², {klasse_erde})")
fig2.show()

# Verarbeitung und Ausgabe: Jupiter
g_jupiter = 24.79
s_jupiter = berechne_fallhoehe(g_jupiter, t)
klasse_jupiter = klassifiziere_planet(g_jupiter)
fig3 = px.line(x=t, y=s_jupiter,
               labels={"x": "Zeit (s)", "y": "Fallhöhe (m)"},
               title=f"Freier Fall auf Jupiter (g = {g_jupiter} m/s², {klasse_jupiter})")
fig3.show()
```

Nach 10 Sekunden fallen Körper auf dem Mond 81 m, auf der Erde 490 m und auf
Jupiter 1240 m. Die Kurven wachsen quadratisch, was sich im Diagramm an der
charakteristischen Parabelform zeigt. Die Funktion `klassifiziere_planet()`
liefert einen String, der direkt in den f-String für den Diagrammtitel
eingesetzt wird.
````

````{admonition} Übung 9.7 (✩✩✩) Mini-Projekt: Töne und Tonleiter
:class: tip
Töne lassen sich als Sinusschwingungen modellieren:

$$y(t) = \sin(2\pi \cdot f \cdot t)$$

Dabei ist $f$ die Frequenz in Hz und $t$ die Zeit in Sekunden.

**Teil 1: Funktion**

Schreiben Sie eine Funktion `berechne_ton(f_hz, dauer_s)`, die eine Zeitachse
von 0 bis `dauer_s` mit 1000 Punkten und das zugehörige Sinussignal berechnet.
Die Funktion soll beide Arrays zurückgeben. Versehen Sie die Funktion mit einem
Docstring.

**Teil 2: C-Durtonleiter**

Die C-Durtonleiter hat folgende acht Töne:

```python
noten      = ["C4", "D4", "E4", "F4", "G4", "A4", "B4", "C5"]
frequenzen = [261.63, 293.66, 329.63, 349.23, 392.00, 440.00, 493.88, 523.25]
```

Durchlaufen Sie die Frequenzliste mit einer `for`-Schleife und führen Sie
in jedem Durchgang folgende Schritte aus:

1. Berechnen Sie das Signal mit `berechne_ton()` über 10 ms (0.01 s).
2. Klassifizieren Sie den Ton mit `elif` anhand der Frequenz:
   - unter 300 Hz: `"tief"`
   - 300 bis unter 450 Hz: `"mittel"`
   - 450 Hz und mehr: `"hoch"`
3. Geben Sie Notenname, Frequenz und Klasse mit einem f-String formatiert aus.
4. Erstellen Sie ein Liniendiagramm des Tons mit Notenname und Frequenz im Titel.

Verwenden Sie eine Zählvariable für den Zugriff auf die Notennamen.

**Teil 3: Überlagerung zweier Töne**

Berechnen Sie den Kammerton A (440 Hz) und das mittlere C (261.63 Hz) jeweils
über 10 ms. Addieren Sie beide Signale elementweise zu einem Überlagerungssignal
`y_sum = y1 + y2` und visualisieren Sie es in einem eigenen Diagramm.

**Teil 4: Erklärung**

Erklären Sie kurz: Warum reichen 10 ms für eine sinnvolle Darstellung der
Schwingungsform, während in Kapitel 9.2 mehrere Sekunden verwendet wurden?

Strukturieren Sie Ihren Code mit EVA-Kommentaren.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import numpy as np
import plotly.express as px

def berechne_ton(f_hz, dauer_s):
    """Berechnet eine Sinusschwingung für einen Ton.

    f_hz:    Frequenz in Hz
    dauer_s: Dauer in Sekunden
    Rückgabe: t (Zeitachse), y (Sinussignal), jeweils als NumPy-Array
    """
    t = np.linspace(0, dauer_s, 1000)
    y = np.sin(2 * np.pi * f_hz * t)
    return t, y

# Eingabe
noten      = ["C4", "D4", "E4", "F4", "G4", "A4", "B4", "C5"]
frequenzen = [261.63, 293.66, 329.63, 349.23, 392.00, 440.00, 493.88, 523.25]
DAUER_S    = 0.01   # 10 Millisekunden

# Verarbeitung und Ausgabe: Tonleiter
i = 0
for f in frequenzen:
    t_ton, y_ton = berechne_ton(f, DAUER_S)

    if f < 300:
        klasse = "tief"
    elif f < 450:
        klasse = "mittel"
    else:
        klasse = "hoch"

    print(f"{noten[i]}: {f:.2f} Hz ({klasse})")

    fig = px.line(x=t_ton * 1000, y=y_ton,
                  labels={"x": "Zeit (ms)", "y": "Amplitude"},
                  title=f"{noten[i]} ({f:.2f} Hz)")
    fig.show()

    i = i + 1

# Verarbeitung und Ausgabe: Überlagerung
t1, y1 = berechne_ton(440.00, DAUER_S)
t2, y2 = berechne_ton(261.63, DAUER_S)
y_sum  = y1 + y2

fig_sum = px.line(x=t1 * 1000, y=y_sum,
                  labels={"x": "Zeit (ms)", "y": "Amplitude"},
                  title="Überlagerung: A4 (440 Hz) + C4 (261.63 Hz)")
fig_sum.show()
```

Ausgabe (Auszug):
```
C4: 261.63 Hz (tief)
D4: 293.66 Hz (tief)
E4: 329.63 Hz (mittel)
F4: 349.23 Hz (mittel)
G4: 392.00 Hz (mittel)
A4: 440.00 Hz (mittel)
B4: 493.88 Hz (hoch)
C5: 523.25 Hz (hoch)
```

4. Bei 440 Hz enthält ein Zeitfenster von 10 ms genau 4.4 vollständige
   Schwingungen. Das reicht aus, um die Kurvenform klar zu sehen. Bei 10
   Sekunden würden 4400 Schwingungen übereinander gezeichnet, was im Diagramm
   nur als gefüllter Balken aussähe. In Kapitel 9.2 interessierte dagegen das
   langsame Abklingen der Amplitude über mehrere Sekunden. Die Zeitskala richtet
   sich immer nach dem zu beobachtenden Phänomen.

Das Überlagerungssignal entsteht durch elementweise Addition der beiden Arrays.
Die Kurve ist komplexer als ein einfacher Sinus und zeigt das typische Muster
einer Schwebung: Die Amplitude schwankt rhythmisch, weil sich die beiden
Frequenzen abwechselnd verstärken und auslöschen.
````

