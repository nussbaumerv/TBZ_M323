# Lösungen zu den FlatMap-Übungen

## Übung 1

**Aufgabe:** Zahlen in Unterlisten verdoppeln und zu einer flachen Liste zusammenfügen.

**Lösung:**

```scala
val listen = List(List(1, 2), List(3, 4), List(5, 6))
val verdoppelt = listen.flatMap(unterliste => unterliste.map(zahl => zahl * 2))

println(verdoppelt)
```

**Erklärung:**

1.  **`flatMap(unterliste => ...)`**:  `flatMap` kombiniert `map` und `flatten`.
2.  **`unterliste.map(zahl => zahl * 2)`**:  *Innerhalb* von `flatMap` wenden wir `map` auf jede *Unterliste* an.  Das verdoppelt die Zahlen in der *Unterliste*.  Das Ergebnis wäre eine *Liste von Listen*.
3.  `flatMap` "flacht" diese Liste von Listen ab:  Es kombiniert die Ergebnisse der `map`-Aufrufe zu einer *einzigen*, flachen Liste.

## Übung 2

**Aufgabe:** Liste aller einzigartigen Lieblingsfarben.

**Lösung:**

```scala
val personen = List(("Max", List("Blau", "Grün")), ("Anna", List("Rot")), ("Julia", List("Gelb", "Blau", "Grün")))
val farben = personen.flatMap(person => person._2).distinct

println(farben)
```

**Erklärung:**

1.  **`personen.flatMap(person => person._2)`**:
    *   `person._2` greift auf das *zweite* Element des Tupels `person` zu (die Liste der Farben).
    *   `flatMap` wendet dies auf jedes Tupel an und kombiniert die Farblisten zu einer einzigen, flachen Liste.
2.  **`.distinct`**: Entfernt *Duplikate* aus der Liste.  Das Ergebnis ist eine Liste einzigartiger Farben.
