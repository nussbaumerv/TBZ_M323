# Lösungen zu den FoldLeft-Übungen

## Übung 1

**Aufgabe:** Summe aller Zahlen in `List(1, 2, 3, 4, 5)` mit `foldLeft` berechnen.

**Lösung:**

```scala
val zahlen = List(1, 2, 3, 4, 5)
val summe = zahlen.foldLeft(0)((akkumulator, zahl) => akkumulator + zahl)

println(summe)
```

**Erklärung:**

1.  **`foldLeft(0)`**:
    *   `foldLeft` nimmt einen *Startwert* (hier `0`).
    *   Und eine *Funktion*, die zwei Argumente entgegennimmt.
2.  Die Funktion `(akkumulator, zahl) => akkumulator + zahl` :
    *   `akkumulator`: Der aktuelle Zwischenwert (am Anfang der Startwert).
    *   `zahl`: Das aktuelle Element der Liste.
    *   `akkumulator + zahl`: Addiert den aktuellen Wert zum Zwischenwert.  Das *Ergebnis* wird zum *neuen* Zwischenwert.
3. `foldLeft` "faltet" die Liste von links nach rechts, wobei in jedem Schritt der Zwischenwert aktualisiert wird.

## Übung 2

**Aufgabe:** Kombinieren aller Strings in `List("Hallo", " ", "Welt", "!")` zu einem String.

**Lösung:**

```scala
val strings = List("Hallo", " ", "Welt", "!")
val kombiniert = strings.foldLeft("")((akkumulator, str) => akkumulator + str)

println(kombiniert)
```

**Erklärung:**

*   Startwert ist ein leerer String `""`.
*   Die Funktion hängt das aktuelle String-Element (`str`) an den Akkumulator an.

## Übung 3

**Aufgabe:** Schwerpunkt von Punkten berechnen.

**Lösung:**

```scala
val points = List((1, 3), (2, 5), (4, 8), (6, 2))

val (sumX, sumY, count) = points.foldLeft((0, 0, 0)) { case ((sumX, sumY, count), (x, y)) =>
  (sumX + x, sumY + y, count + 1)
}

val schwerpunkt = (sumX.toDouble / count, sumY.toDouble / count)
println(schwerpunkt)
```

**Erklärung:**

1.  **`foldLeft((0, 0, 0))`**: Startwert ist ein Tupel `(sumX, sumY, count)`.  Wir brauchen *drei* Werte, um den Schwerpunkt zu berechnen.
2.  **`case ((sumX, sumY, count), (x, y)) => ...`**:
    *   `case` erlaubt *Pattern Matching* auf Tupeln.  Das ist sehr praktisch, um die einzelnen Werte zu "entpacken".
    *   `(sumX, sumY, count)`:  Das aktuelle Tupel mit den Zwischenwerten.
    *   `(x, y)`: Das aktuelle Punkt-Tupel.
    * `(sumX + x, sumY + y, count + 1)`: Berechnet die neuen Zwischenwerte und gibt ein *neues* Tupel zurück.
3. Nach `foldLeft` haben wir die *Summen* und die *Anzahl*.
4.  `sumX.toDouble / count`:  Berechnet den Durchschnitt der x- und y-Koordinaten.  Wir wandeln `sumX` in `Double` um, um eine Fliesskommadivision zu erhalten (wichtig!).
