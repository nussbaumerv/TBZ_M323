# Lösungen zu den Filter-Übungen

## Übung 1

**Aufgabe:** Behalten nur der geraden Zahlen aus `List(1, 2, 3, 4, 5)`.

**Lösung:**

```scala
val zahlen = List(1, 2, 3, 4, 5)
val geradeZahlen = zahlen.filter(zahl => zahl % 2 == 0)

println(geradeZahlen)
```

**Erklärung:**

1.  `filter` nimmt eine Funktion entgegen, die `true` oder `false` zurückgibt.
2.  `zahl % 2 == 0` prüft, ob die Zahl gerade ist (Rest bei Division durch 2 ist 0).
3.  Nur wenn die Funktion `true` ergibt, wird das Element in die neue Liste übernommen.

## Übung 2

**Aufgabe:** Auswahl von Namen mit mehr als vier Buchstaben aus `List("Alice", "Bob", "Charlie", "Diana")`.

**Lösung:**

```scala
val namen = List("Alice", "Bob", "Charlie", "Diana")
val langeNamen = namen.filter(name => name.length > 4)

println(langeNamen)
```

**Erklärung:**
`name.length` gibt die Länge (Anzahl Zeichen) eines Strings.

## Übung 3

**Aufgabe:** Behalten aller Zahlen größer als 50 aus `List(12, 45, 68, 100)`.

**Lösung:**

```scala
val zahlen = List(12, 45, 68, 100)
val grosseZahlen = zahlen.filter(zahl => zahl > 50)

println(grosseZahlen)
```

## Übung 4

**Aufgabe:** Behalten aller Wörter, die mit "S" beginnen, aus `List("Scala", "ist", "fantastisch")`.

**Lösung:**

```scala
val woerter = List("Scala", "ist", "fantastisch")
val woerterMitS = woerter.filter(wort => wort.startsWith("S"))

println(woerterMitS)
```
**Erklärung:**
`wort.startsWith("S")` ist die Funktion der Klasse String, die testet, ob der String mit "S" beginnt.

## Übung 5

**Aufgabe:** Liste der Titel aller Bücher, die vor 1950 veröffentlicht wurden.

**Lösung:**

```scala
case class Buch(titel: String, autor: String, jahr: Int)

val buecher = List(
  Buch("1984", "George Orwell", 1949),
  Buch("Brave New World", "Aldous Huxley", 1932),
  Buch("Fahrenheit 451", "Ray Bradbury", 1953)
)

val titelVor1950 = buecher.filter(buch => buch.jahr < 1950).map(buch => buch.titel)

println(titelVor1950)
```

**Erklärung:**

1.  **`buecher.filter(buch => buch.jahr < 1950)`:**  Filtert zuerst die Bücher, deren `jahr` kleiner als 1950 ist.  Das Ergebnis ist eine Liste von `Buch`-Objekten.
2.  **`.map(buch => buch.titel)`:**  Wendet dann `map` auf diese gefilterte Liste an, um nur die `titel` der Bücher zu extrahieren.