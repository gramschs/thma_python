# Übungen

````{admonition} Optional: Übung 9.8 (✩✩✩)
:class: tip
Der mittlere Temperaturverlauf eines Jahres lässt sich als Sinusfunktion über
12 Monate modellieren. Wir simulieren außerdem natürliche Schwankungen durch
Rauschen.

Die Formel für den monatlichen Temperaturverlauf lautet:

$$T(m) = T_{avg} + A \cdot \sin\left(\frac{2\pi}{12} \cdot (m - m_{max})\right) + \epsilon$$

Dabei ist $m$ die Monatszahl (0 bis 11), $m_{max} = 6.5$ der Monat mit der
höchsten Temperatur (Juli) und $\epsilon$ ein normalverteiltes Rauschen mit
Standardabweichung 1.5 °C.

Verwenden Sie $T_{avg} = 10.0$ °C und $A = 9.0$ °C.

1. Schreiben Sie eine Funktion `berechne_jahrestemperatur(T_avg, A, m)`, die
   den Temperaturverlauf ohne Rauschen berechnet und zurückgibt. `m` ist ein
   NumPy-Array. Versehen Sie die Funktion mit einem Docstring.
2. Erzeugen Sie ein Array `m` mit den Monatszahlen 0 bis 11 (verwenden Sie
   `np.linspace(0, 11, 12)`). Berechnen Sie das Temperatur-Array und fügen Sie
   Rauschen hinzu.
3. Visualisieren Sie den Temperaturverlauf als Liniendiagramm. Verwenden Sie
   als x-Achse folgende Monatsnamen-Liste:
   ```python
   monate = ["Jan", "Feb", "Mär", "Apr", "Mai", "Jun",
             "Jul", "Aug", "Sep", "Okt", "Nov", "Dez"]
   ```
4. Durchlaufen Sie das Temperatur-Array mit einer `for`-Schleife und
   klassifizieren Sie jeden Monat mit `elif`:
   - unter 5 °C: `"Winter"`
   - 5 bis unter 15 °C: `"Übergang"`
   - 15 °C und mehr: `"Sommer"`
   Geben Sie Monatsnamen und Klassifikation aus. Verwenden Sie eine
   Zählvariable für den Zugriff auf die Monatsnamen.
5. Geben Sie die Temperatur im Dezember (letzter Wert) und im November
   (vorletzter Wert) mit negativem Index und f-String formatiert aus.

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

def berechne_jahrestemperatur(T_avg, A, m):
    """Berechnet den mittleren monatlichen Temperaturverlauf in °C.

    T_avg: mittlere Jahrestemperatur in °C
    A:     Amplitude in °C
    m:     Monatszahl als NumPy-Array (0 = Januar, 11 = Dezember)
    """
    return T_avg + A * np.sin(2 * np.pi / 12 * (m - 6.5))

# Eingabe
T_avg  = 10.0
A      = 9.0
monate = ["Jan", "Feb", "Mär", "Apr", "Mai", "Jun",
          "Jul", "Aug", "Sep", "Okt", "Nov", "Dez"]

# Verarbeitung
m        = np.linspace(0, 11, 12)
T_sauber = berechne_jahrestemperatur(T_avg, A, m)
rauschen = np.random.normal(0, 1.5, 12)
T        = T_sauber + rauschen

# Ausgabe: Liniendiagramm
fig = px.line(x=monate, y=T,
              labels={"x": "Monat", "y": "Temperatur (°C)"},
              title="Simulierter Jahrestemperaturverlauf")
fig.show()

# Ausgabe: Klassifikation
i = 0
for temp in T:
    if temp < 5.0:
        klasse = "Winter"
    elif temp < 15.0:
        klasse = "Übergang"
    else:
        klasse = "Sommer"
    print(f"{monate[i]}: {temp:.1f} °C ({klasse})")
    i = i + 1

# Ausgabe: Jahresende
print(f"Temperatur im Dezember:  {T[-1]:.1f} °C")
print(f"Temperatur im November:  {T[-2]:.1f} °C")
```

Die Klassifikation zeigt das typische mitteleuropäische Muster: Winter in den
Monaten Dezember bis Februar, Sommer von Juni bis August, Übergang im Frühjahr
und Herbst. Das Rauschen sorgt dafür, dass die Grenzen nicht immer exakt
eingehalten werden. Durch den negativen Index `T[-1]` und `T[-2]` kann auf
die letzten beiden Monatswerte zugegriffen werden, ohne die genaue Länge des
Arrays zu kennen.
````

````{admonition} Optional: Übung 9.9 (✩✩✩) Mini-Projekt: Schwingungsanalyse eines Stoßdämpfers
:class: tip
In dieser Aufgabe analysieren Sie das Schwingungsverhalten eines Stoßdämpfers
unter verschiedenen Bedingungen. Sie kombinieren dabei Funktionen, Schleifen,
Bedingungen, Rauschen und NumPy-Arrays.

**Teil 1: Funktion implementieren**

Schreiben Sie eine Funktion `berechne_daempfung(t, A_m, f_hz, delta)`, die
eine gedämpfte Schwingung berechnet und zurückgibt. Verwenden Sie die Formel
aus Kapitel 9.2 und versehen Sie die Funktion mit einem Docstring.

**Teil 2: Klassifikation**

Schreiben Sie eine Funktion `klassifiziere_daempfung(delta)`, die den
Dämpfungskoeffizienten $\delta$ bewertet und eine Zeichenkette zurückgibt:
- kleiner als 0.5 s⁻¹: `"schwach gedämpft"`
- zwischen 0.5 und 2.0 s⁻¹: `"mittel gedämpft"`
- größer als 2.0 s⁻¹: `"stark gedämpft"`

**Teil 3: Simulation**

Verwenden Sie folgende Parameter: $A = 0.08$ m, $f = 1.5$ Hz,
Simulationsdauer 6 s. Durchlaufen Sie mit einer `for`-Schleife die folgenden
drei Dämpfungskoeffizienten:

```python
delta_werte = [0.3, 1.2, 3.0]
```

Führen Sie in jedem Schleifendurchgang folgende Schritte aus:
1. Klassifizieren Sie den Dämpfungskoeffizienten mit `klassifiziere_daempfung()`.
2. Berechnen Sie das Schwingungssignal und addieren Sie Rauschen mit
   Standardabweichung 0.003 m.
3. Berechnen Sie die Einhüllende: `einhuelle = A_m * np.exp(-delta * t)`.
4. Bestimmen Sie mit einer inneren `for`-Schleife und einem Flag die
   Abklingzeit: den ersten Zeitpunkt, an dem die Einhüllende unter 1 mm
   (0.001 m) fällt. Initialisieren Sie `abklingzeit = -1.0` und
   `gefunden = False`. Verwenden Sie eine Zählvariable für den Zugriff
   auf `t`.
5. Erstellen Sie ein Liniendiagramm des verrauschten Signals.
6. Geben Sie eine Zeile der Ergebnistabelle mit f-String formatiert aus.

**Teil 4: Ergebnistabelle**

Die Ausgabe soll folgendes Format haben:
```
delta = 0.3 s⁻¹ (schwach gedämpft):   Abklingzeit = 23.0 s
delta = 1.2 s⁻¹ (mittel gedämpft):    Abklingzeit =  5.7 s
delta = 3.0 s⁻¹ (stark gedämpft):     Abklingzeit =  2.3 s
```

Hinweis: Falls die Abklingzeit innerhalb der 6 Sekunden nicht erreicht wird,
geben Sie `"nicht erreicht"` aus.

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

def berechne_daempfung(t, A_m, f_hz, delta):
    """Berechnet eine gedämpfte Schwingung.

    t:     Zeitachse als NumPy-Array in s
    A_m:   Amplitude in m
    f_hz:  Frequenz in Hz
    delta: Dämpfungskoeffizient in 1/s
    """
    omega = 2 * np.pi * f_hz
    return A_m * np.exp(-delta * t) * np.cos(omega * t)

def klassifiziere_daempfung(delta):
    """Klassifiziert den Dämpfungskoeffizienten eines Stoßdämpfers."""
    if delta < 0.5:
        return "schwach gedämpft"
    elif delta <= 2.0:
        return "mittel gedämpft"
    else:
        return "stark gedämpft"

# Eingabe
A_m         = 0.08    # Amplitude in m
f_hz        = 1.5     # Frequenz in Hz
delta_werte = [0.3, 1.2, 3.0]
t           = np.linspace(0, 6, 1000)

# Verarbeitung und Ausgabe
for delta in delta_werte:
    # Klassifikation
    klasse = klassifiziere_daempfung(delta)

    # Signal mit Rauschen
    x          = berechne_daempfung(t, A_m, f_hz, delta)
    rauschen   = np.random.normal(0, 0.003, len(t))
    x_verrauscht = x + rauschen

    # Einhüllende und Abklingzeit
    einhuelle  = A_m * np.exp(-delta * t)
    abklingzeit = -1.0
    gefunden   = False
    i = 0
    for e in einhuelle:
        if e < 0.001 and gefunden == False:
            abklingzeit = t[i]
            gefunden = True
        i = i + 1

    # Diagramm
    fig = px.line(x=t, y=x_verrauscht,
                  labels={"x": "Zeit (s)", "y": "Auslenkung (m)"},
                  title=f"Stoßdämpfer: delta = {delta} s⁻¹ ({klasse})")
    fig.show()

    # Tabelle
    if gefunden == True:
        print(f"delta = {delta} s⁻¹ ({klasse}):   Abklingzeit = {abklingzeit:.1f} s")
    else:
        print(f"delta = {delta} s⁻¹ ({klasse}):   Abklingzeit = nicht erreicht")
```

Die äußere Schleife durchläuft die drei Dämpfungskoeffizienten. Die innere
Schleife sucht mithilfe eines Flags (`gefunden`) nach dem ersten Zeitpunkt,
an dem die Einhüllende unter die 1-mm-Grenze fällt. Ohne das Flag würde
`abklingzeit` bei jedem weiteren Unterschreiten überschrieben werden. Mit dem
Flag stoppt die Suche nach dem ersten Treffer, auch wenn die Schleife noch
weiterläuft. Bei $\delta = 0.3$ s⁻¹ wird die Grenze innerhalb von 6 s
möglicherweise nicht erreicht, was korrekt als "nicht erreicht" ausgegeben wird.
````
