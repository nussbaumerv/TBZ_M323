# Lösungen zu For Comprehensions

## Übung 1

**Aufgabe:** Zahlen von 1 bis 10 quadrieren.

**Lösung:**

```scala
val zahlen = 1 to 10
val quadrate = for (zahl <- zahlen) yield zahl * zahl

println(quadrate)
```

**Erklärung:**

1.  **`for (zahl <- zahlen)`**:  Das ist die grundlegende Syntax einer for-Comprehension.  Sie durchläuft die Elemente von `zahlen` (jedes Element wird `zahl`).
2.  **`yield zahl * zahl`**:  `yield` *erzeugt* einen Wert für *jedes* Element.  Hier wird die Zahl quadriert.  Das Ergebnis ist eine *neue* Sammlung (hier eine Liste) mit den quadrierten Zahlen.

    *For-Comprehensions sind im Grunde "syntaktischer Zucker" für Kombinationen von `map`, `flatMap` und `filter`.*

## Übung 2

**Aufgabe:** Gerade Zahlen von 1 bis 20 auswählen.

**Lösung:**

```scala
val zahlen = 1 to 20
val geradeZahlen = for (zahl <- zahlen if zahl % 2 == 0) yield zahl

println(geradeZahlen)
```

**Erklärung:**

*   **`if zahl % 2 == 0`**:  Dies ist ein *Filter* innerhalb der for-Comprehension.  Nur wenn die Bedingung `true` ist, wird der `yield`-Teil ausgeführt.

## Übung 3

**Aufgabe:** Alle Paare aus Farben und Früchten generieren.

**Lösung:**

```scala
val colors = List("Red", "Green", "Blue")
val fruits = List("Apple", "Banana", "Orange")

val paare = for {
  farbe <- colors
  frucht <- fruits
} yield (farbe, frucht)

println(paare)
```

**Erklärung:**

1.  **`farbe <- colors`**:  Durchläuft alle Farben.
2.  **`frucht <- fruits`**:  Für *jede* Farbe werden *alle* Früchte durchlaufen. Das ist eine *verschachtelte* Iteration.
3.  **`yield (farbe, frucht)`**:  Erzeugt ein Tupel `(farbe, frucht)` für jede Kombination.

## Übung 4

**Aufgabe:** Kombinationen von Benutzer und nicht abgeschlossener Aufgabe.

**Lösung:**

```scala
case class User(name: String, tasks: List[String])

val users = List(
  User("Alice", List("Task 1", "Task 2", "Task 3")),
  User("Bob", List("Task 1", "Task 4", "Task 5")),
  User("Charlie", List("Task 2", "Task 3", "Task 6"))
)

val tasksCompleted = List("Task 1", "Task 3", "Task 5")

val pendingTasks = for {
    user <- users
    task <- user.tasks
    if !tasksCompleted.contains(task)
} yield (user.name, task)

println(pendingTasks)
```

**Erklärung:**

1. **`user <- users`**: Durchläuft alle Benutzer.
2. **`task <- user.tasks`**: Durchläuft alle Aufgaben des *aktuellen* Benutzers.
3. **`if !tasksCompleted.contains(task)`**:
    *   `tasksCompleted.contains(task)`: Prüft, ob die aktuelle Aufgabe in der Liste der abgeschlossenen Aufgaben enthalten ist.
    *   `!` negiert das Ergebnis (also: "wenn die Aufgabe *nicht* abgeschlossen ist").
4.  **`yield (user.name, task)`**:  Erzeugt ein Tupel aus Benutzername und nicht abgeschlossener Aufgabe.
