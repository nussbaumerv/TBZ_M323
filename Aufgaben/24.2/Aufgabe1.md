# Aufgabe 1 - Beispiele umsetzen als Funktionen (Reise planen)

**Funktionen identifizieren:**

Basierend auf der Beschreibung "Reise planen" können wir folgende Funktionen ableiten:

* **`addDestination(route: List[String], destination: String): List[String]`**: Fügt eine Destination zu einer bestehenden Route hinzu.
* **`removeDestination(route: List[String], destination: String): List[String]`**: Entfernt eine Destination aus einer Route.
* **`changeDestination(route: List[String], oldDestination: String, newDestination: String): List[String]`**: Ersetzt eine Destination in der Route durch eine neue.
* **`createRoute(destinations: List[String]): List[String]`**: Erstellt eine neue Route aus einer Liste von Destinationen. (Diese Funktion ist eigentlich trivial, da eine Liste direkt als Route dienen kann, aber der Vollständigkeit halber).

**Scala Code:**

```scala
object Reiseplanung {

  def addDestination(route: List[String], destination: String): List[String] = {
    route :+ destination // Fügt am Ende der Liste hinzu (Reihenfolge wichtig bei Routen)
  }

  def removeDestination(route: List[String], destination: String): List[String] = {
    route.filterNot(_ == destination) // Behält alle Destinationen außer der angegebenen
  }

  def changeDestination(route: List[String], oldDestination: String, newDestination: String): List[String] = {
    route.map {
      case dest if dest == oldDestination => newDestination // Ersetzt die alte durch die neue Destination
      case dest => dest // Behält die Destination bei, wenn sie nicht die alte ist
    }
  }

  def createRoute(destinations: List[String]): List[String] = {
    destinations // Eine Liste von Strings IST bereits eine Route
  }

  def main(args: Array[String]): Unit = {
    val initialRoute = List("Paris", "Rom", "Berlin")
    println(s"Start Route: ${initialRoute}")

    val routeWithNewDestination = addDestination(initialRoute, "Wien")
    println(s"Route mit Wien hinzugefügt: ${routeWithNewDestination}")

    val routeWithoutRom = removeDestination(routeWithNewDestination, "Rom")
    println(s"Route ohne Rom: ${routeWithoutRom}")

    val routeWithChangedDestination = changeDestination(routeWithoutRom, "Berlin", "Hamburg")
    println(s"Route mit Berlin zu Hamburg geändert: ${routeWithChangedDestination}")
  }
}
```

**Erläuterung:**

* **Deklarativer Ansatz:**  Wir beschreiben *was* wir mit der Route machen wollen (Destination hinzufügen, entfernen, ändern) und nicht *wie* (z.B. mit Schleifen und Indexmanipulationen).
* **Funktionen sind rein:** Die Funktionen nehmen eine Route (Liste) entgegen und geben eine *neue* Route (Liste) zurück. Sie verändern nicht die ursprüngliche Route (Immutability - ein wichtiges Konzept in der funktionalen Programmierung).
* **Scala List API:**  Wir nutzen die mächtigen Funktionen der Scala `List` API wie `:+` (hinzufügen), `filterNot` (filtern), und `map` (transformieren), um die Logik deklarativ auszudrücken.

## Aufgabe 2 - "Wörter mit Punkten bewerten"

**Funktionen identifizieren:**

* **`scoreWord(word: String): Int`**: Berechnet die Punktzahl eines Wortes.
* **`sortWordsByScore(words: List[String]): List[String]`**: Sortiert eine Liste von Wörtern nach ihrer Punktzahl (absteigend).

**Scala Code:**

```scala
object WoerterBewerten {

  def scoreWord(word: String): Int = {
    word.toLowerCase().count(_ != 'a') // Zählt Buchstaben, die nicht 'a' sind (case-insensitive)
  }

  def sortWordsByScore(words: List[String]): List[String] = {
    words.sortBy(scoreWord).reverse // Sortiert zuerst aufsteigend nach Score und kehrt dann um (absteigend)
  }

  def main(args: Array[String]): Unit = {
    val words = List("Haus", "Auto", "Banane", "Apfel", "Zug")
    println(s"Unsortierte Wörter: ${words}")

    val scoredWords = words.map(word => (word, scoreWord(word))) // Wort und Score Paare erstellen
    println(s"Wörter mit Scores: ${scoredWords}")

    val sortedWords = sortWordsByScore(words)
    println(s"Sortierte Wörter nach Score (absteigend): ${sortedWords}")
  }
}
```

**Erläuterung:**

* **`scoreWord` Funktion:**
    * `word.toLowerCase()`: Macht das Wort klein, damit 'A' und 'a' gleich behandelt werden.
    * `count(_ != 'a')`:  Iteriert über jeden Buchstaben (`_`) im Wort und zählt, wie viele Buchstaben *nicht* gleich 'a' sind.
* **`sortWordsByScore` Funktion:**
    * `words.sortBy(scoreWord)`: Sortiert die Liste der Wörter basierend auf dem Ergebnis der `scoreWord` Funktion für jedes Wort. Standardmäßig sortiert `sortBy` aufsteigend.
    * `.reverse`: Kehrt die sortierte Liste um, um eine absteigende Sortierung (höchster Score zuerst) zu erreichen.

## Aufgabe 3 - "Autorennen"

**Funktionen identifizieren:**

* **`calculateTotalRaceTime(lapTimes: List[Double]): Double`**: Berechnet die Gesamtrennzeit aus einer Liste von Rundenzeiten.
* **`calculateAverageLapTime(lapTimes: List[Double]): Double`**: Berechnet die Durchschnittsrundenzeit (ohne Warm-up Runde).

**Scala Code:**

```scala
object Autorennen {

  def calculateTotalRaceTime(lapTimes: List[Double]): Double = {
    if (lapTimes.isEmpty) 0.0 // Schutz vor leerer Liste
    else lapTimes.tail.sum // `.tail` entfernt die erste Runde (Warm-up), dann summiert
  }

  def calculateAverageLapTime(lapTimes: List[Double]): Double = {
    val raceLapTimes = lapTimes.tail // Rundenzeiten ohne Warm-up
    if (raceLapTimes.isEmpty) 0.0 // Schutz vor leerer Liste nach Entfernen der ersten Runde
    else raceLapTimes.sum / raceLapTimes.length // Summe der Rundenzeiten geteilt durch Anzahl der Runden
  }

  def main(args: Array[String]): Unit = {
    val car1LapTimes = List(65.5, 62.3, 61.8, 62.9, 63.1) // Beispiel: Warm-up Runde + 4 Rennrunden
    println(s"Rundenzeiten Auto 1: ${car1LapTimes}")

    val totalTimeCar1 = calculateTotalRaceTime(car1LapTimes)
    println(s"Gesamtrennzeit Auto 1: ${totalTimeCar1} Sekunden")

    val averageLapTimeCar1 = calculateAverageLapTime(car1LapTimes)
    println(s"Durchschnittliche Rundenzeit Auto 1: ${averageLapTimeCar1} Sekunden")

    val car2LapTimes = List(70.1, 63.5, 62.7, 63.8) // Beispiel für ein anderes Auto
    println(s"\nRundenzeiten Auto 2: ${car2LapTimes}")

    val totalTimeCar2 = calculateTotalRaceTime(car2LapTimes)
    println(s"Gesamtrennzeit Auto 2: ${totalTimeCar2} Sekunden")

    val averageLapTimeCar2 = calculateAverageLapTime(car2LapTimes)
    println(s"Durchschnittliche Rundenzeit Auto 2: ${averageLapTimeCar2} Sekunden")
  }
}
```

**Erläuterung:**

* **`calculateTotalRaceTime` Funktion:**
    * `lapTimes.tail`:  `.tail` gibt eine neue Liste zurück, die alle Elemente der ursprünglichen Liste enthält, außer dem ersten Element.  Dadurch wird die Warm-up Runde (die erste Runde) entfernt.
    * `.sum`: Summiert alle verbleibenden Rundenzeiten.
* **`calculateAverageLapTime` Funktion:**
    * `lapTimes.tail`: Entfernt wieder die Warm-up Runde.
    * `raceLapTimes.sum / raceLapTimes.length`: Berechnet den Durchschnitt, indem die Summe der Rennrundenzeiten durch die Anzahl der Rennrunden geteilt wird.
* **Fehlerbehandlung (leere Liste):** In beiden Funktionen wird ein Fall für leere Listen abgefangen, um Fehler zu vermeiden und `0.0` zurückzugeben, falls keine Rundenzeiten vorhanden sind.


**Wichtig:**

* **Funktionale Reinheit:** Alle Funktionen sind rein. Sie verändern keine Eingabeparameter und geben immer basierend auf den Eingaben das gleiche Ergebnis zurück.
* **Deklarativer Stil:** Der Code konzentriert sich auf *was* berechnet werden soll, nicht auf die genauen Schritte *wie* es berechnet wird (z.B. keine expliziten Schleifenindizes).
* **Scala List Funktionen:**  Die Nutzung von `tail`, `sum`, `length`, `map`, `filterNot`, `sortBy` usw. aus der Scala Collections API macht den Code sehr prägnant und lesbar.

Ich hoffe, diese Lösungen helfen dir weiter und verdeutlichen den deklarativen Ansatz in der funktionalen Programmierung! Lass mich wissen, wenn du noch Fragen hast oder etwas ändern möchtest.