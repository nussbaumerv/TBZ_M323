# Lösungen zu den Map-Übungen

## Übung 1

**Aufgabe:** Verdoppeln jeder Zahl in der Liste `List(1, 2, 3, 4, 5)`.

**Lösung:**

```scala
val zahlen = List(1, 2, 3, 4, 5)
val verdoppelteZahlen = zahlen.map(zahl => zahl * 2)

println(verdoppelteZahlen)
```

**Erklärung:**

1.  Wir erstellen eine Liste `zahlen`.
2.  Wir verwenden die `map`-Funktion. Sie nimmt eine Funktion als Argument entgegen.
3.  Die Funktion `zahl => zahl * 2` wird auf *jedes* Element der Liste angewendet.
    *   `zahl` ist der Platzhalter für das aktuelle Element.
    *   `zahl * 2` verdoppelt das aktuelle Element.
4. Das Resultat ist eine *neue* Liste aller verdoppelter Zahlen.


## Übung 2

**Aufgabe:** Umwandeln jedes Namens in der Liste `List("Alice", "Bob", "Charlie")` in Großbuchstaben.

**Lösung:**

```scala
val namen = List("Alice", "Bob", "Charlie")
val grossbuchstabenNamen = namen.map(name => name.toUpperCase)

println(grossbuchstabenNamen)
```

**Erklärung:**
`name.toUpperCase` ist die Funktion der Klasse String, die den String in Grossbuchstaben konvertiert.

## Übung 3

**Aufgabe:** Berechnen der Hälfte jeder Zahl in der Liste `List(12, 45, 68, 100)`.

**Lösung:**

```scala
val zahlen = List(12, 45, 68, 100)
val halbeZahlen = zahlen.map(zahl => zahl / 2.0)

println(halbeZahlen)
```

**Erklärung:**

Wichtig ist, dass wir durch `2.0` (eine Double-Zahl) teilen, und nicht durch `2`. Ansonsten wird eine Integer-Division durchgeführt.

## Übung 4

**Aufgabe:** Erstellen einer Liste formatierter Adress-Strings.

**Lösung:**

```scala
case class Adresse(strasse: String, hausnummer: Int, postleitzahl: String, stadt: String)

val adressen = List(
  Adresse("Hauptstrasse", 10, "12345", "Musterstadt"),
  Adresse("Nebenstrasse", 5, "23456", "Beispielburg")
)

val formatierteAdressen = adressen.map(adresse => s"${adresse.strasse} ${adresse.hausnummer}, ${adresse.postleitzahl} ${adresse.stadt}")

println(formatierteAdressen)
```

**Erklärung:**

*   Wir verwenden String-Interpolation (`s"..."`), um die Adressbestandteile zu einem String zusammenzufügen.
* `${...}` erlaubt es, Variablen direkt in den String einzubetten.

## Übung 5

**Aufgabe:** Erstellen einer Liste der Vornamen in Großbuchstaben.

**Lösung:**

```scala
val namen = List("Max Mustermann", "Erika Mustermann")

val vornamenGross = namen.map(name => name.split(" ").head.toUpperCase)
println(vornamenGross)
```

**Erklärung:**

1.  `name.split(" ")`: Teilt den String `name` bei jedem Leerzeichen auf und gibt ein Array von Strings zurück (z.B. `Array("Max", "Mustermann")`).
2.  `.head`: Nimmt das erste Element dieses Arrays (also den Vornamen).
3. `.toUpperCase`: Konvertiert den Vornamen in Großbuchstaben.
