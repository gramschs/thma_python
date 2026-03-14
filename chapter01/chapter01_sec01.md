---
kernelspec:
  name: python3
  display_name: 'Python 3'
---

# 1.1 Algorithmus und Programmiersprachen

Es gibt viele Gründe, warum es sich lohnt, Programmieren zu lernen. Die
Nachfrage nach Ingenieurinnen und Ingenieuren, die zusätzlich Programmieren
können, wächst aufgrund der Digitalisierung der Industrie rasant. Programmieren
fördert kritisches Denken und Problemlösungsfähigkeiten. Umgekehrt werden durch
Programmieren diese Fähigkeiten weiter entwickelt. Zudem fördert Programmieren
das Verständnis von Technologie und Computersystemen. Es kann helfen, die
Funktionsweise von Software und Hardware besser zu verstehen und Einblicke in
die Arbeitsweise von Websites, Anwendungen und anderen Technologien zu gewinnen.
Programmierung kann auch dabei helfen, Routineaufgaben zu automatisieren und
Zeit zu sparen. Dies kann Fehler minimieren und die Effizienz steigern.

## Lernziele

```{admonition} Lernziele
:class: attention
* [ ] Sie können erklären, was ein **Algorithmus** ist.
* [ ] Sie wissen, was eine **Programmiersprache** ist.
* [ ] Sie kennen den Unterschied zwischen **höheren Programmiersprachen** und
  **Maschinensprache**.
* [ ] Sie wissen, was der Unterschied zwischen einer **kompilierten
  Programmiersprache** und einer **interpretierten Programmiersprache** ist. Sie
  können für beide Kategorien Beispiele benennen.
```

## Algorithmus

Programmieren bedeutet, dem Computer eine Reihe von Anweisungen zu geben. Es
geht darum, mit Hilfe einer Abfolge von Anweisungen ein Problem zu lösen. Ein
wichtiger Aspekt des Programmierens ist die Fähigkeit, komplexe Probleme in
kleinere, leichter zu lösende Aufgaben zu unterteilen. Diese Aufgaben können
dann einzeln gelöst und in einem größeren Programm kombiniert werden, um das
Problem als Ganzes zu lösen.

Diese schrittweise Beschreibung der Lösung eines Problems nennt man
**Algorithmus**. Ein Algorithmus ist ein klar definierter Satz von Anweisungen
oder Regeln, die von einem Computer (oder auch von einem Menschen) ausgeführt
werden können, um ein bestimmtes Ergebnis zu erzielen.

Ein Beispiel aus dem Alltag ist die Steuerung eines Fahrstuhls:

* Jemand drückt im Erdgeschoss den Knopf.
* Der Fahrstuhl fährt nach unten, hält an, und die Tür öffnet sich.
* Die Person steigt ein und wählt die 3. Etage.
* Der Fahrstuhl schließt die Tür, fährt hoch bis zur 3. Etage, hält wieder an,
  öffnet die Tür und die Person steigt aus.

```{admonition} Mini-Übung
:class: tip
Nehmen Sie sich 5 Minuten Zeit und schreiben Sie die Schritte auf, die ein
Fahrstuhl befolgen muss, um eine Person vom Erdgeschoss in die 2. Etage zu
bringen.
```

```{admonition} Lösung
:class: tip 
:class: dropdown
1. Warte auf Knopfdruck im Erdgeschoss.
2. Fahre ins Erdgeschoss (falls nicht schon dort).
3. Öffne Tür.
4. Warte, bis Person eingestiegen ist.
5. Schließe Tür.
6. Fahre in die 2. Etage.
7. Öffne Tür.
8. Warte, bis Person ausgestiegen ist.
9. Schließe Tür.
```

Die obige Lösung funktioniert nur für den Transport vom Erdgeschoss in die 2.
Etage. Ein echter Fahrstuhl-Algorithmus muss aber allgemeiner sein und für
beliebige Start- und Zieletagen funktionieren. Das folgende Flussdiagramm zeigt
einen solchen allgemeinen Algorithmus:

```{mermaid}
flowchart TD
    A[Start: Fahrstuhl wartet] --> B{Knopf außen gedrückt?}
    B -->|Nein| B
    B -->|Ja| C[Fahre zu der Etage mit dem Knopf]
    C --> D[Öffne Tür]
    D --> E{Person eingestiegen?}
    E -->|Nein| E
    E -->|Ja| F[Schließe Tür]
    F --> G{Ziel-Knopf innen gedrückt?}
    G -->|Nein| G
    G -->|Ja| H[Fahre zur Ziel-Etage]
    H --> I[Öffne Tür]
    I --> J{Person ausgestiegen?}
    J -->|Nein| J
    J -->|Ja| K[Schließe Tür]
    K --> A
    
    style A fill:#e1f5fe
    style B fill:#fff3e0
    style E fill:#fff3e0
    style G fill:#fff3e0
    style J fill:#fff3e0
```

In dem Flussdiagramm stehen die Rauten für Entscheidungen und die Rechtecke für
Aktionen. Der Pfeil zurück zum Start zeigt: Ein Fahrstuhl arbeitet in einer
Endlosschleife und wartet kontinuierlich auf neue Anfragen.

Die Beschreibung kann unterschiedlich detailliert sein. Zum Beispiel kann man
präzisieren, wie lange die Tür geöffnet bleiben soll oder was passiert, wenn
gleichzeitig andere Knöpfe gedrückt werden. Hier erkennt man: Ein Algorithmus
kann sehr einfach beginnen, aber durch zusätzliche Fälle immer komplexer werden.

```{admonition} Mini-Übung
:class: tip
Überlegen Sie, welche zusätzlichen Regeln notwendig wären, wenn der Fahrstuhl
gleichzeitig mehrere Anfragen erhält (z. B. jemand möchte in die 4. Etage und
jemand anders in die 2. Etage).
```

```{admonition} Lösung
:class: tip 
:class: dropdown
* Der Fahrstuhl muss entscheiden, in welcher Reihenfolge die Stockwerke
  angefahren werden.  
* Mögliches Vorgehen: Immer in der aktuellen Fahrtrichtung alle Stockwerke
  bedienen, bevor gewendet wird.  
* Beispiel: Wenn der Fahrstuhl im Erdgeschoss startet und Knöpfe für die 2. und
  4. Etage gedrückt sind, fährt er zuerst zur 2., dann zur 4. Etage.  
```

Auf die Idee, Alltagsprozesse in Form eines Algorithmus zu beschreiben, werden
wir in späteren Kapiteln zurückkehren. Als nächstes beschäftigen wir uns damit,
wie dem Computer solche Anweisungen in einer Programmiersprache erteilt werden.

## Programmiersprachen

Eine **Programmiersprache** ist eine formale Sprache, mit der sich
Datenstrukturen und Algorithmen beschreiben lassen, sodass ein Computer diese
Anweisungen ausführen kann.

Es gibt nicht die *eine* wichtigste oder beste Programmiersprache. Welche
Sprache man verwendet, hängt immer von der Anwendung ab. Für ein
Smartphone-Spiel wird eine andere Sprache gewählt als für die numerische
Simulation in den Ingenieurwissenschaften. Einen Überblick über die Beliebtheit
von Programmiersprachen bietet der sogenannte *Tiobe-Index*:

> [https://www.tiobe.com/tiobe-index/](https://www.tiobe.com/tiobe-index/)

```{admonition} Mini-Übung
:class: tip
Recherchieren Sie im Tiobe-Index nach den Programmiersprachen MATLAB und Python.

1. Auf welchem Platz stehen die beiden Programmiersprachen aktuell?
2. Schauen Sie sich auch die langfristige Entwicklung an. Wie haben sich beide
   Sprachen in den letzten 10 Jahren entwickelt?
```

```{admonition} Lösung
:class: tip 
:class: dropdown
1. Python steht typischerweise in den Top 3, MATLAB meist zwischen Platz 15-20.
2. Python zeigt seit Jahren einen deutlichen Aufwärtstrend, während MATLAB
   stagniert oder leicht rückläufig ist.
```

Besonders für Ingenieurstudierende stellt sich oft die Frage: MATLAB oder
Python? Während MATLAB traditionell in vielen technischen Fächern gelehrt wird,
zeigt die Entwicklung der letzten Jahre einen klaren Trend zu Python. Dies liegt
nicht nur an der größeren Vielseitigkeit, sondern auch daran, dass
Python-Kenntnisse weit über die Ingenieurwissenschaften hinaus wertvoll sind.

In der Anfangszeit der Computer waren Programmiersprachen noch sehr nah an der
**Maschinensprache**. Maschinensprache besteht aus *Binärcode* (Nullen und
Einsen), den der Prozessor direkt ausführt. Hier ein Beispiel in *Assembler*,
einer sehr maschinenorientierten Sprache, die bereits schwer lesbar ist:

```{figure} https://gramschs.github.io/thma_python_assets/pics/chapter01/fig_assembler.png
:name: fig_chap00_sec01

"Hallo Welt" in Assembler
(Quelle: [Wikipedia → Assemblersprache](https://de.wikipedia.org/wiki/Assemblersprache))
```

In einer modernen Sprache wie Python ist der gleiche Code deutlich kürzer
und leichter verständlich:

```{code-cell} python
print('Hallo Welt')
```

Heute arbeiten wir fast ausschließlich mit den sogenannten **höheren
Programmiersprachen** (wie Python, MATLAB oder C++), die für Menschen leichter
verständlich sind. Damit Computer diese Anweisungen ausführen können, müssen sie
aber trotzdem in Maschinensprache übersetzt werden. Das geschieht auf zwei
Arten:

* **Compiler-Sprachen**: Der gesamte Code wird vorab in Maschinensprache
übersetzt. Der Übersetzungsvorgang heißt Kompilieren.
* **Interpreter-Sprachen**: Der Code wird erst beim Ausführen Zeile für Zeile in
Maschinensprache übersetzt. Der zeilenweise Ausführung wird Interpretieren
genannt.

Manchmal wird kompilierter Code als Programm und interpretierter Code als Skript
bezeichnet. Im Alltag ist diese Unterscheidung aber nicht immer wichtig; oft
sagt man zu beidem schlicht »Programm«.

```{admonition} Mini-Übung
:class: tip
Ordnen Sie die folgenden Programmiersprachen zu: Sind sie kompiliert oder
interpretiert?

* C bzw. C++  
* C# (ausgesprochen: C Sharp)  
* JavaScript
* Python
* Visual Basic  
```

```{admonition} Lösung
:class: tip 
:class: dropdown
* C bzw. C++ → kompiliert  
* C# → kompiliert
* JavaScript → interpretiert 
* Python → interpretiert
* Visual Basic → kompiliert  
```

Insgesamt ist der Unterschied zwischen kompilierten und interpretierten Sprachen
vor allem eine Frage der Geschwindigkeit und Flexibilität. Kompilierte Programme
sind in der Regel schneller als interpretierte Programme, da der Maschinencode
direkt vom Betriebssystem ausgeführt werden kann. Umgekehrt können Änderungen
des Programms bei interpretierten Programmen schneller durchgeführt werden, da
diese ja ohnehin Zeile für Zeile abgearbeitet und interpretiert werden. Dies
bedeutet, dass Änderungen am Code sofort wirksam werden, ohne dass eine erneute
Kompilierung erforderlich ist.

Letztendlich hängt die Wahl der Programmiersprache von den Anforderungen des
Projekts ab und davon, welche Kompromisse zwischen Geschwindigkeit und
Flexibilität akzeptabel sind.

## Warum Python?

Was ist überhaupt Python? Wikipedia beschreibt Python so:

> "Python ([ˈpʰaɪθn̩], [ˈpʰaɪθɑn], auf Deutsch auch [ˈpʰyːtɔn]) ist eine
  universelle, üblicherweise interpretierte, höhere Programmiersprache. Sie hat
  den Anspruch, einen gut lesbaren, knappen Programmierstil zu fördern. So
  werden beispielsweise Blöcke nicht durch geschweifte Klammern, sondern durch
  Einrückungen strukturiert."
  (Quelle: [Wikipedia](https://de.wikipedia.org/wiki/Python_(Programmiersprache)))

In dieser Vorlesung verwenden wir Python als Programmiersprache, da Python viele
Vorteile für den Einstieg bietet:

1. *Einfache Syntax*: Python hat eine klare und leicht verständliche Syntax, die
   es leicht macht, die Grundlagen der Programmierung zu erlernen. Die Syntax
   ist lesbar und ähnelt der englischen Sprache, was das Verständnis
   erleichtert.
2. *Vielseitigkeit*: Python ist eine sehr vielseitige Programmiersprache, die in
   vielen verschiedenen Bereichen eingesetzt werden kann. Sie wird oft für
   Datenanalyse, künstliche Intelligenz, Webentwicklung und wissenschaftliches
   Rechnen verwendet.
3. *Große Community*: Python hat eine große Community von Entwicklern, die aktiv
   an der Weiterentwicklung der Sprache und an der Bereitstellung von
   Hilfestellung und Ressourcen für Anfänger beteiligt sind. Es gibt viele
   Online-Foren, Kurse und Tutorials, die das Erlernen der Sprache erleichtern.
4. *Interaktiver Modus*: Python bietet einen interaktiven Modus, der es
   Anfängern ermöglicht, Code Zeile für Zeile auszuführen und das Ergebnis
   sofort zu sehen. Dies macht das Experimentieren und die Suche nach Fehlern im
   Code sehr einfach und effektiv.
5. *Plattformunabhängigkeit*: Python kann auf verschiedenen Betriebssystemen wie
   Windows, Mac und Linux ausgeführt werden.

Das Erlernen einer Programmiersprache ist ein bisschen wie das Lernen einer
Fremdsprache: Die erste ist die schwierigste. Danach fällt der Umstieg auf
andere Sprachen wesentlich leichter.

## Zusammenfassung und Ausblick

In diesem Kapitel haben wir die Vorteile des Programmierens für Ingenieure
diskutiert, den Begriff des Algorithmus anhand der Fahrstuhlsteuerung eingeführt
und die Unterschiede zwischen verschiedenen Programmiersprachen erklärt.
Außerdem haben wir gesehen, warum Python als erste Sprache besonders geeignet
ist. Im nächsten Kapitel beschäftigen wir uns mit den technischen
Voraussetzungen, um eigene Python-Programme zu schreiben, und benutzen Python
als Taschenrechner.
