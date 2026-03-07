---
kernelspec:
  name: python3
  display_name: 'Python 3'
---

# Übungen

````{admonition} Übung 8.1 (✩)
:class: tip
Gegeben ist folgender Code:

```python
PI = 3.141592653589793

def berechne_kreisflaeche(r_m):
    return PI * r_m**2

def berechne_kreisumfang(r_m):
    return 2 * PI * r_m

r = 5
flaeche = berechne_kreisflaeche(r)
umfang = berechne_kreisumfang(r)
```

1. Sagen Sie vorher, welche Werte `flaeche` und `umfang` nach der Ausführung
   enthalten. Notieren Sie Ihre Antwort, bevor Sie den Code ausführen.
2. Führen Sie den Code aus und überprüfen Sie Ihre Vorhersage.
3. Erklären Sie: Was ist der Unterschied zwischen dem Parameter `r_m` in der
   Funktionsdefinition und dem Argument `r` beim Aufruf?
4. Was gibt `type(berechne_kreisflaeche(5))` zurück? Überlegen Sie zuerst.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
1. Vorhersage:
   - `flaeche` = PI * 25 ≈ 78.54
   - `umfang` = 2 * PI * 5 ≈ 31.42

2. Code zur Überprüfung:
```python
PI = 3.141592653589793

def berechne_kreisflaeche(r_m):
    return PI * r_m**2

def berechne_kreisumfang(r_m):
    return 2 * PI * r_m

r = 5
flaeche = berechne_kreisflaeche(r)
umfang = berechne_kreisumfang(r)
print(flaeche)   # 78.53981633974483
print(umfang)    # 31.41592653589793
```

3. Erklärung: `r_m` ist der formale **Parameter** in der Funktionsdefinition.
   Er ist ein Platzhalter und hat nur innerhalb der Funktion Bedeutung. `r`
   ist das konkrete **Argument** beim Aufruf, also der tatsächliche Wert, der
   an die Funktion übergeben wird. Beim Aufruf `berechne_kreisflaeche(r)`
   nimmt der Parameter `r_m` den Wert von `r`, also `5`, an.

4. `type(berechne_kreisflaeche(5))` gibt `<class 'float'>` zurück, da
   `PI` ein Float ist und das Ergebnis der Berechnung ebenfalls ein Float.
````

````{admonition} Übung 8.2 (✩)
:class: tip
Schreiben Sie eine Funktion `zeige_trennlinie()`, die eine Zeile mit 40
Gleichheitszeichen ausgibt:

```
========================================
```

Verwenden Sie in der Funktion den Multiplikationsoperator `*` für Strings
(z.B. `"=" * 40`). Die Funktion hat weder Parameter noch Rückgabewert.

Testen Sie die Funktion, indem Sie sie dreimal hintereinander aufrufen. Rufen
Sie sie anschließend in einer for-Schleife fünfmal auf und beobachten Sie die
Ausgabe.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
def zeige_trennlinie():
    print("=" * 40)

# Dreimaliger Aufruf
zeige_trennlinie()
zeige_trennlinie()
zeige_trennlinie()

# Aufruf in Schleife
for i in range(5):
    zeige_trennlinie()
```

Ausgabe der drei Aufrufe:
```
========================================
========================================
========================================
```

Erklärung: Die Funktionsdefinition mit `def` führt die Funktion noch nicht aus.
Sie legt lediglich fest, was beim Aufruf passieren soll. Erst der Aufruf
`zeige_trennlinie()` führt den Code im Funktionsrumpf aus. Da die Funktion
keinen Rückgabewert hat, gibt sie automatisch `None` zurück. Das stört hier
nicht, weil wir das Ergebnis nirgends speichern. Würden Sie
`print(zeige_trennlinie())` schreiben, würde zusätzlich `None` angezeigt.
````

````{admonition} Übung 8.3 (✩)
:class: tip
Das Volumen eines Zylinders berechnet sich nach:

$$V = \pi \cdot r^2 \cdot h$$

wobei $r$ der Radius in Metern und $h$ die Höhe in Metern ist.

Schreiben Sie eine Funktion `berechne_volumen_zylinder(r_m, h_m)`, die das
Volumen in Kubikmetern zurückgibt. Versehen Sie die Funktion mit einem
einzeiligen Docstring.

Berechnen Sie anschließend das Volumen für folgende drei Zylinder und geben
Sie die Ergebnisse mit f-Strings formatiert aus:

| Zylinder | Radius | Höhe |
|----------|--------|------|
| Drucktank A | 0.5 m | 2.0 m |
| Drucktank B | 0.3 m | 1.5 m |
| Drucktank C | 0.8 m | 0.6 m |

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

def berechne_volumen_zylinder(r_m, h_m):
    """Berechnet das Volumen eines Zylinders in Kubikmetern."""
    return np.pi * r_m**2 * h_m

# Verarbeitung und Ausgabe
V_A = berechne_volumen_zylinder(0.5, 2.0)
print(f"Drucktank A: r = 0.5 m,  h = 2.0 m,  V = {V_A:.4f} m³")

V_B = berechne_volumen_zylinder(0.3, 1.5)
print(f"Drucktank B: r = 0.3 m,  h = 1.5 m,  V = {V_B:.4f} m³")

V_C = berechne_volumen_zylinder(0.8, 0.6)
print(f"Drucktank C: r = 0.8 m,  h = 0.6 m,  V = {V_C:.4f} m³")
```

Ausgabe:
```
Drucktank A: r = 0.5 m,  h = 2.0 m,  V = 1.5708 m³
Drucktank B: r = 0.3 m,  h = 1.5 m,  V = 0.4241 m³
Drucktank C: r = 0.8 m,  h = 0.6 m,  V = 1.2063 m³
```

Erklärung: Die Funktion kapselt die Formel und kann beliebig oft mit
verschiedenen Argumenten aufgerufen werden. Der Docstring erscheint, wenn
man `help(berechne_volumen_zylinder)` aufruft.
````

````{admonition} Übung 8.4 (✩✩)
:class: tip
Der Wirkungsgrad einer Maschine gibt an, welcher Anteil der zugeführten
Energie als Nutzenergie abgegeben wird:

$$\eta = \frac{P_{nutz}}{P_{zu}} \cdot 100$$

wobei $P_{nutz}$ die Nutzleistung in kW und $P_{zu}$ die zugeführte Leistung
in kW ist. Das Ergebnis ist der Wirkungsgrad in Prozent.

Schreiben Sie eine Funktion `berechne_wirkungsgrad(P_nutz_kW, P_zu_kW)`, die
den Wirkungsgrad in Prozent zurückgibt. Versehen Sie die Funktion mit einem
Docstring.

Berechnen Sie den Wirkungsgrad für folgende vier Maschinen und geben Sie die
Ergebnisse aus.

| Maschine | Nutzleistung | Zugeführte Leistung |
|----------|-------------|---------------------|
| Elektromotor | 18.5 kW | 20.0 kW |
| Verbrennungsmotor | 55.0 kW | 180.0 kW |
| Hydraulikpumpe | 7.2 kW | 8.5 kW |
| Dampfturbine | 420.0 kW | 1200.0 kW |

Strukturieren Sie Ihren Code mit EVA-Kommentaren.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
def berechne_wirkungsgrad(P_nutz_kW, P_zu_kW):
    """Berechnet den Wirkungsgrad einer Maschine in Prozent."""
    return P_nutz_kW / P_zu_kW * 100

# Verarbeitung und Ausgabe
eta = berechne_wirkungsgrad(18.5, 20.0)
print(f"Elektromotor:        {eta:.1f} %")

eta = berechne_wirkungsgrad(55.0, 180.0)
print(f"Verbrennungsmotor:   {eta:.1f} %")

eta = berechne_wirkungsgrad(7.2, 8.5)
print(f"Hydraulikpumpe:      {eta:.1f} %")

eta = berechne_wirkungsgrad(420.0, 1200.0)
print(f"Dampfturbine:        {eta:.1f} %")
```

Ausgabe:
```
Elektromotor:        92.5 %
Verbrennungsmotor:   30.6 %
Hydraulikpumpe:      84.7 %
Dampfturbine:        35.0 %
```

Ausgabe:
```
Maschine               P_nutz      P_zu  Wirkungsgrad
--------------------------------------------------------
Elektromotor            18.5 kW    20.0 kW        92.5 %
Verbrennungsmotor       55.0 kW   180.0 kW        30.6 %
Hydraulikpumpe           7.2 kW     8.5 kW        84.7 %
Dampfturbine           420.0 kW  1200.0 kW        35.0 %
```

Erklärung: Der Verbrennungsmotor hat mit ca. 30 % den schlechtesten
Wirkungsgrad. Der Elektromotor gibt mit 92.5 % fast die gesamte zugeführte
Energie als Nutzleistung ab. Die Funktion wird viermal mit denselben
Formeln aufgerufen, ohne dass die Berechnung wiederholt werden muss.
````

````{admonition} Übung 8.5 (✩✩)
:class: tip
Schreiben Sie eine Funktion `berechne_kreis(r_m)`, die sowohl den Umfang als
auch die Fläche eines Kreises berechnet und beide Werte zurückgibt.

Die Formeln lauten:

$$U = 2 \pi r \qquad A = \pi r^2$$

Versehen Sie die Funktion mit einem Docstring, der beide Rückgabewerte
beschreibt.

Rufen Sie die Funktion für die Radien 0.1 m, 0.5 m, 1.0 m, 2.0 m und 5.0 m
auf. Geben Sie die Ergebnisse formnatiert aus.

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

def berechne_kreis(r_m):
    """Berechnet Umfang und Fläche eines Kreises.

    Rückgabe: umfang_m (float), flaeche_m2 (float)
    """
    umfang_m = 2 * np.pi * r_m
    flaeche_m2 = np.pi * r_m**2
    return umfang_m, flaeche_m2

# Verarbeitung und Ausgabe
U, A = berechne_kreis(0.1)
print(f"r = 0.1 m:  Umfang = {U:.3f} m,  Fläche = {A:.3f} m²")

U, A = berechne_kreis(0.5)
print(f"r = 0.5 m:  Umfang = {U:.3f} m,  Fläche = {A:.3f} m²")

U, A = berechne_kreis(1.0)
print(f"r = 1.0 m:  Umfang = {U:.3f} m,  Fläche = {A:.3f} m²")

U, A = berechne_kreis(2.0)
print(f"r = 2.0 m:  Umfang = {U:.3f} m,  Fläche = {A:.3f} m²")

U, A = berechne_kreis(5.0)
print(f"r = 5.0 m:  Umfang = {U:.3f} m,  Fläche = {A:.3f} m²")
```

Ausgabe:
```
r = 0.1 m:  Umfang = 0.628 m,  Fläche = 0.031 m²
r = 0.5 m:  Umfang = 3.142 m,  Fläche = 0.785 m²
r = 1.0 m:  Umfang = 6.283 m,  Fläche = 3.142 m²
r = 2.0 m:  Umfang = 12.566 m,  Fläche = 12.566 m²
r = 5.0 m:  Umfang = 31.416 m,  Fläche = 78.540 m²
```

Erklärung: Beim Aufruf `U, A = berechne_kreis(0.1)` werden die zwei
Rückgabewerte der Funktion direkt zwei Variablen zugewiesen. Das funktioniert,
weil Python bei mehreren Rückgabewerten intern die Werte der Reihe nach den
Variablen links des `=` zuordnet.
````

````{admonition} Übung 8.6 (✩✩)
:class: tip
Gegeben sind folgende drei Funktionen ohne Docstring:
```python
import numpy as np

def f1(m_kg, v_ms):
    return 0.5 * m_kg * v_ms**2

def f2(m_kg, g_ms2, h_m):
    return m_kg * g_ms2 * h_m

def f3(U_V, I_A):
    return U_V * I_A
```

1. Ergänzen Sie jede Funktion mit einem einzeiligen Docstring, der beschreibt,
   was die Funktion berechnet und welche Einheit der Rückgabewert hat.
2. Rufen Sie für jede Funktion `help()` auf und überprüfen Sie, ob Ihr
   Docstring verständlich ist.
3. Berechnen Sie mit den drei Funktionen:
   - Kinetische Energie eines Fahrzeugs mit 1200 kg bei 100 km/h
     (Achtung: Umrechnung in m/s erforderlich: $v = 100 / 3.6$)
   - Potentielle Energie einer Masse von 50 kg in 10 m Höhe
     ($g = 9.81 \, \text{m/s}^2$)
   - Elektrische Leistung bei 230 V und 16 A
4. Geben Sie die drei Ergebnisse mit f-Strings formatiert aus.

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

def f1(m_kg, v_ms):
    """Berechnet die kinetische Energie in Joule: E_kin = 0.5 * m * v^2."""
    return 0.5 * m_kg * v_ms**2

def f2(m_kg, g_ms2, h_m):
    """Berechnet die potentielle Energie in Joule: E_pot = m * g * h."""
    return m_kg * g_ms2 * h_m

def f3(U_V, I_A):
    """Berechnet die elektrische Leistung in Watt: P = U * I."""
    return U_V * I_A

# Docstrings anzeigen
help(f1)
help(f2)
help(f3)

# Eingabe
v_ms = 100 / 3.6

# Verarbeitung
E_kin_J = f1(1200, v_ms)
E_pot_J = f2(50, 9.81, 10)
P_W = f3(230, 16)

# Ausgabe
print(f"Kinetische Energie:   {E_kin_J:.1f} J")
print(f"Potentielle Energie:  {E_pot_J:.1f} J")
print(f"Elektrische Leistung: {P_W:.1f} W")
```

Ausgabe:
```
Kinetische Energie:   462963.0 J
Potentielle Energie:  4905.0 J
Elektrische Leistung: 3680.0 W
```

Erklärung: Der Docstring wird direkt nach der `def`-Zeile in dreifachen
Anführungszeichen geschrieben und bei `help()` angezeigt. So sind eigene
Funktionen genauso dokumentiert wie eingebaute Python-Funktionen.
````

````{admonition} Übung 8.7 (✩✩)
:class: tip
Das Hookesche Gesetz beschreibt den linearen Zusammenhang zwischen der
Auslenkung einer Feder und der rücktreibenden Kraft: $F = k \cdot x$, wobei
$k$ die Federkonstante in N/m und $x$ die Auslenkung in m ist.

Schreiben Sie eine Funktion `berechne_federkraft(k_nm, x_m)`, die die
Federkraft in Newton zurückgibt. Versehen Sie die Funktion mit einem Docstring.

Erstellen Sie anschließend drei separate Liniendiagramme für die drei
Federkonstanten:

| Feder | Federkonstante |
|-------|----------------|
| Weiche Feder | 200 N/m |
| Mittlere Feder | 500 N/m |
| Steife Feder | 1000 N/m |

Verwenden Sie Auslenkungen von 0 m bis 0.20 m in Schritten von 0.01 m.
Erstellen Sie für jede Feder eine eigene Liste mit Kräften und ein eigenes
Diagramm mit passendem Titel.

Strukturieren Sie Ihren Code mit EVA-Kommentaren.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import plotly.express as px

def berechne_federkraft(k_nm, x_m):
    """Berechnet die Federkraft in Newton nach dem Hookeschen Gesetz F = k * x."""
    return k_nm * x_m

# Verarbeitung
auslenkungen   = []
kraefte_weich  = []
kraefte_mittel = []
kraefte_steif  = []

for i in range(0, 21):
    x = i * 0.01
    auslenkungen.append(x)
    kraefte_weich.append(berechne_federkraft(200, x))
    kraefte_mittel.append(berechne_federkraft(500, x))
    kraefte_steif.append(berechne_federkraft(1000, x))

# Ausgabe
fig1 = px.line(x=auslenkungen, y=kraefte_weich,
               labels={"x": "Auslenkung (m)", "y": "Federkraft (N)"},
               title="Federkennlinie: k = 200 N/m (weich)")
fig1.show()

fig2 = px.line(x=auslenkungen, y=kraefte_mittel,
               labels={"x": "Auslenkung (m)", "y": "Federkraft (N)"},
               title="Federkennlinie: k = 500 N/m (mittel)")
fig2.show()

fig3 = px.line(x=auslenkungen, y=kraefte_steif,
               labels={"x": "Auslenkung (m)", "y": "Federkraft (N)"},
               title="Federkennlinie: k = 1000 N/m (steif)")
fig3.show()
```

Erklärung: Jede Kennlinie wird als eigenes Diagramm ausgegeben. Alle drei
sind Geraden durch den Ursprung: Je größer die Federkonstante, desto steiler
die Linie. Der Vergleich ergibt sich durch die unterschiedlichen Maximalwerte
auf der y-Achse.
````

````{admonition} Übung 8.8 (✩✩✩)
:class: tip
Wer wissen möchte, was ein Haushaltsgerät im Jahr an Strom kostet, braucht
zwei Formeln:

$$E = \frac{P \cdot t}{1000} \qquad K = E \cdot p$$

wobei $P$ die Leistung in Watt, $t$ die Betriebszeit in Stunden, $E$ der
Verbrauch in Kilowattstunden und $p$ der Strompreis in €/kWh ist.

1. Schreiben Sie eine Funktion `berechne_verbrauch(leistung_W, stunden)`, die
   den Stromverbrauch in kWh zurückgibt. Versehen Sie sie mit einem Docstring.
2. Schreiben Sie eine Funktion `berechne_kosten(kWh, preis_euro)`, die die
   Stromkosten in Euro zurückgibt. Versehen Sie sie mit einem Docstring.
3. Schreiben Sie eine Funktion `berechne_jahreskosten(leistung_W,
   stunden_pro_tag, preis_euro)`, die `berechne_verbrauch()` und
   `berechne_kosten()` aufruft und die jährlichen Stromkosten zurückgibt.
4. Berechnen Sie die Jahreskosten für folgende Geräte bei einem Strompreis
   von 0.32 €/kWh und geben Sie die Ergebnisse mit f-Strings aus:

| Gerät | Leistung | Betrieb pro Tag |
|-------|----------|-----------------|
| Kühlschrank | 150 W | 24 h |
| Waschmaschine | 2000 W | 1 h |
| Fernseher | 120 W | 4 h |
| Kaffeemaschine | 1500 W | 0.5 h |

5. Visualisieren Sie die Jahreskosten als Balkendiagramm.

Strukturieren Sie Ihren Code mit EVA-Kommentaren.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import plotly.express as px

def berechne_verbrauch(leistung_W, stunden):
    """Berechnet den Stromverbrauch in kWh: E = P * t / 1000."""
    return leistung_W * stunden / 1000

def berechne_kosten(kWh, preis_euro):
    """Berechnet die Stromkosten in Euro: K = E * p."""
    return kWh * preis_euro

def berechne_jahreskosten(leistung_W, stunden_pro_tag, preis_euro):
    """Berechnet die jährlichen Stromkosten eines Geräts in Euro."""
    verbrauch_jahr = berechne_verbrauch(leistung_W, stunden_pro_tag * 365)
    return berechne_kosten(verbrauch_jahr, preis_euro)

# Eingabe
PREIS = 0.32   # €/kWh

# Verarbeitung
kosten_kuehlschrank   = berechne_jahreskosten(150,  24,  PREIS)
kosten_waschmaschine  = berechne_jahreskosten(2000,  1,  PREIS)
kosten_fernseher      = berechne_jahreskosten(120,   4,  PREIS)
kosten_kaffeemaschine = berechne_jahreskosten(1500, 0.5, PREIS)

# Ausgabe: Tabelle
print(f"Kühlschrank:    {kosten_kuehlschrank:.2f} €/Jahr")
print(f"Waschmaschine:  {kosten_waschmaschine:.2f} €/Jahr")
print(f"Fernseher:      {kosten_fernseher:.2f} €/Jahr")
print(f"Kaffeemaschine: {kosten_kaffeemaschine:.2f} €/Jahr")

# Ausgabe: Balkendiagramm
geraete  = ["Kühlschrank", "Waschmaschine", "Fernseher", "Kaffeemaschine"]
jahreskosten = [kosten_kuehlschrank, kosten_waschmaschine,
                kosten_fernseher, kosten_kaffeemaschine]

fig = px.bar(x=geraete, y=jahreskosten,
             labels={"x": "Gerät", "y": "Jahreskosten (€)"},
             title=f"Stromkosten pro Jahr (Strompreis: {PREIS} €/kWh)")
fig.show()
```

Ausgabe:
```
Kühlschrank:    420.48 €/Jahr
Waschmaschine:  233.60 €/Jahr
Fernseher:      56.06 €/Jahr
Kaffeemaschine: 87.60 €/Jahr
```

Erklärung: `berechne_jahreskosten()` ruft intern zwei weitere Funktionen auf.
Die Betriebszeit pro Jahr ergibt sich aus `stunden_pro_tag * 365` und wird
direkt als Argument an `berechne_verbrauch()` übergeben. Obwohl die
Waschmaschine mit 2000 W viel mehr Leistung hat als der Kühlschrank, verursacht
der Kühlschrank doppelt soviele Jahreskosten, weil er rund um die Uhr läuft.
````

````{admonition} Übung 8.9 (✩✩✩) Mini-Projekt
:class: tip
In der Physik und Technik gibt es verschiedene Arten von Leistung. In dieser
Aufgabe implementieren Sie vier Formeln als Funktionen und vergleichen die
Ergebnisse für konkrete Szenarien.

**Teil 1: Funktionen implementieren**

Schreiben Sie folgende vier Funktionen, jeweils mit Docstring:

1. `berechne_leistung_mechanisch(F_N, v_ms)`: mechanische Leistung
   $P = F \cdot v$ in Watt
2. `berechne_leistung_elektrisch(U_V, I_A)`: elektrische Leistung
   $P = U \cdot I$ in Watt
3. `berechne_leistung_hydraulisch(p_Pa, Q_m3s)`: hydraulische Leistung
   $P = p \cdot Q$ in Watt
4. `berechne_leistung_thermisch(m_kgs, c_Jkg, delta_T)`: thermische Leistung
   $P = \dot{m} \cdot c \cdot \Delta T$ in Watt, wobei $\dot{m}$ der
   Massenstrom in kg/s und $c$ die spezifische Wärmekapazität in J/(kg·K) ist

**Teil 2: Szenarien berechnen**

Berechnen Sie die Leistung für folgende vier Szenarien:

| Szenario | Funktion | Eingabewerte |
|----------|----------|--------------|
| Elektromotor | elektrisch | 400 V, 25 A |
| Hydraulikzylinder | hydraulisch | 150 bar = 15.000.000 Pa, 0.002 m³/s |
| Antriebswelle | mechanisch | 800 N, 5 m/s |
| Kühlwasserkreislauf | thermisch | 2.0 kg/s, 4182 J/(kg·K), 5 K |

**Teil 3: Ausgabe und Visualisierung**

Geben Sie die vier Ergebnisse mit f-Strings formatiert aus:
```
Elektromotor:          10000.0 W
Hydraulikzylinder:     30000.0 W
Antriebswelle:          4000.0 W
Kühlwasserkreislauf:   41820.0 W
```

Visualisieren Sie die vier Leistungswerte als Balkendiagramm. Strukturieren
Sie Ihren Code mit EVA-Kommentaren.
````

```{code-cell} python
# Code-Zelle
```

````{admonition} Lösung
:class: tip
:class: dropdown
```python
import plotly.express as px

def berechne_leistung_mechanisch(F_N, v_ms):
    """Berechnet die mechanische Leistung in Watt: P = F * v."""
    return F_N * v_ms

def berechne_leistung_elektrisch(U_V, I_A):
    """Berechnet die elektrische Leistung in Watt: P = U * I."""
    return U_V * I_A

def berechne_leistung_hydraulisch(p_Pa, Q_m3s):
    """Berechnet die hydraulische Leistung in Watt: P = p * Q."""
    return p_Pa * Q_m3s

def berechne_leistung_thermisch(m_kgs, c_Jkg, delta_T):
    """Berechnet die thermische Leistung in Watt: P = m_dot * c * delta_T."""
    return m_kgs * c_Jkg * delta_T

# Verarbeitung
P_elektrisch  = berechne_leistung_elektrisch(400, 25)
P_hydraulisch = berechne_leistung_hydraulisch(15_000_000, 0.002)
P_mechanisch  = berechne_leistung_mechanisch(800, 5)
P_thermisch   = berechne_leistung_thermisch(2.0, 4182, 5)

# Ausgabe: Tabelle
print(f"Elektromotor:          {P_elektrisch:>8.1f} W")
print(f"Hydraulikzylinder:     {P_hydraulisch:>8.1f} W")
print(f"Antriebswelle:         {P_mechanisch:>8.1f} W")
print(f"Kühlwasserkreislauf:   {P_thermisch:>8.1f} W")

# Ausgabe: Balkendiagramm
szenarien  = ["Elektromotor", "Hydraulikzylinder", "Antriebswelle", "Kühlwasserkreislauf"]
leistungen = [P_elektrisch, P_hydraulisch, P_mechanisch, P_thermisch]

fig = px.bar(x=szenarien, y=leistungen,
             labels={"x": "Szenario", "y": "Leistung (W)"},
             title="Leistungsvergleich verschiedener physikalischer Systeme")
fig.show()
```

Ausgabe:
```
Elektromotor:           10000.0 W
Hydraulikzylinder:      30000.0 W
Antriebswelle:           4000.0 W
Kühlwasserkreislauf:    41820.0 W
```

Erklärung: Jede Funktion kapselt genau eine physikalische Formel. Die
vier Ergebnisse werden in separaten Variablen gespeichert und anschließend
für Tabelle und Balkendiagramm verwendet. Das Balkendiagramm zeigt, dass
der Kühlwasserkreislauf mit über 41 kW die größte Leistung transportiert,
während die Antriebswelle mit 4 kW die kleinste aufweist.
````
