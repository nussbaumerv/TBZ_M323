# Lösungen zu Map und Filter (kombiniert)

## Übung 1

**Aufgabe:** Liste der Vornamen (in Großbuchstaben) aller IT-Mitarbeiter mit einem Gehalt von 50000 oder mehr.

**Lösung:**

```scala
case class Mitarbeiter(name: String, abteilung: String, gehalt: Int)

val mitarbeiter = List(
  Mitarbeiter("Max Mustermann", "IT", 50000),
  Mitarbeiter("Erika Musterfrau", "Marketing", 45000),
  Mitarbeiter("Klaus Klein", "IT", 55000),
  Mitarbeiter("Julia Gross", "HR", 40000)
)

val itMitarbeiterVornamen = mitarbeiter
  .filter(ma => ma.abteilung == "IT" && ma.gehalt >= 50000)
  .map(ma => ma.name.split(" ").head.toUpperCase)

println(itMitarbeiterVornamen)
```

**Erklärung:**

1.  **`filter(...)`**: Behält nur Mitarbeiter, bei denen *beide* Bedingungen zutreffen:
    *   `ma.abteilung == "IT"`: Abteilung ist "IT".
    *   `ma.gehalt >= 50000`: Gehalt ist 50000 oder mehr.
2. **`map(...)`**: Extrahiert Vorname, konvertiert in Grossbuchstaben (bereits erklärt).

## Übung 2

**Aufgabe:** Kursnamen filtern, Leerzeichen entfernen und sortieren.

**Lösung:**

```scala
val kurse = List(
  "Programmierung in Scala",
  "Datenbanken",
  "Webentwicklung mit JavaScript",
  "Algorithmen und Datenstrukturen"
)

// 1. Filtern nach "Daten"
val gefilterteKurse = kurse.filter(kurs => kurs.contains("Daten"))

// 2. Leerzeichen entfernen
val ohneLeerzeichen = gefilterteKurse.map(kurs => kurs.replace(" ", ""))

// 3. Alphabetisch sortieren
val sortiert = ohneLeerzeichen.sorted
println(sortiert)

// 4. Umgekehrt alphabetisch sortieren
val umgekehrtSortiert = ohneLeerzeichen.sortWith(_ > _)
println(umgekehrtSortiert)
```

**Erklärung:**

1.  **`filter(kurs => kurs.contains("Daten"))`**:  Behält Kurse, die "Daten" enthalten.  `contains` ist eine String-Methode.
2.  **`map(kurs => kurs.replace(" ", ""))`**: Ersetzt *alle* Vorkommen von " " (Leerzeichen) durch "" (leeren String). `replace` ist eine String Methode.
3. **`sorted`**: Sortiert die Liste in aufsteigender, alphabetischer Reihenfolge. Funktioniert mit Strings "automatisch".
4. **`sortWith(_ > _)`**:
    *   `sortWith` erlaubt das Sortieren mit einer eigenen Vergleichsfunktion.
    *  `_ > _` ist eine Kurzschreibweise für eine Funktion, die zwei Elemente (hier Strings) vergleicht, und `true` liefert, wenn das erste Element *grösser* als das zweite ist.  Dadurch wird absteigend sortiert.
