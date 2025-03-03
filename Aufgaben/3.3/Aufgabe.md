Absolut! Hier ist eine detaillierte Lösung der Aufgaben, inklusive Erklärungen, Code-Beispielen und Hinweisen zur Dokumentation:

**Aufgabe 1 - Pure vs. Impure Funktionen**

Hier ist die Tabelle, die die Analyse der Funktionen zusammenfasst:

| Aufgabe | Nur ein Rückgabewert | Resultat nur abhängig von übergebenen Parametern | Verändert keine existierenden Werte | pure oder impure | Begründung                                                                                                                                                 |
| :------ | :------------------- | :------------------------------------------------- | :------------------------------------ | :--------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.1     | Ja                   | Nein                                               | Nein                                  | impure           | Die Funktion verändert den globalen Zustand (`cartItems`) und das Ergebnis hängt von diesem Zustand ab.                                                  |
| 1.2     | Ja                   | Ja                                                 | Ja                                    | pure             | Alle Regeln für pure Funktionen sind erfüllt.                                                                                                              |
| 1.3     | Ja                   | Ja                                                 | Ja                                    | pure             | Alle Regeln für pure Funktionen sind erfüllt.                                                                                                              |
| 1.4     | Ja                   | Nein                                               | Ja                                    | impure           | Das Ergebnis hängt von `Math.random()` (JavaScript) bzw. `Random.nextDouble()` (Scala) ab, was nicht durch Parameter kontrolliert wird.                       |
| 1.5     | Ja                   | Ja                                                 | Ja                                    | pure             | Alle Regeln für pure Funktionen sind erfüllt.                                                                                                              |
| 1.6     | Ja                   | Ja                                                 | Ja (bedingt*)                                   | impure           | `console.log` (JavaScript) bzw. `println` (Scala) sind Seiteneffekte, da sie die Konsole verändern. Streng genommen ist dies eine Verletzung der Regel. |


**Aufgabe 2 - Umschreiben von Impure zu Pure Functions**

Hier sind die umgeschriebenen Funktionen und die Erklärungen, warum einige Änderungen notwendig sind:

**1.1 - addToCart (Pure Version):**

```javascript
// JavaScript
function addToCartPure(cartItems, item) {
  return [...cartItems, item]; // Neue Liste erstellen, statt die alte zu verändern
}

let myCart = [];
myCart = addToCartPure(myCart, 'Apple');
myCart = addToCartPure(myCart, 'Banana');
console.log(myCart); // Ausgabe: ['Apple', 'Banana']
```

```scala
// Scala
def addToCartPure(cartItems: List[String], item: String): List[String] = {
  cartItems :+ item  // Neue Liste erstellen, statt die alte zu verändern. :+ hängt ein Element an.
}

var myCart = List[String]() //var, da die Referenz auf die Liste sich ändert.
myCart = addToCartPure(myCart, "Apple")
myCart = addToCartPure(myCart, "Banana")
println(myCart)  // Ausgabe: List(Apple, Banana)

```

**Erklärung:**

*   Die *pure* Version nimmt den aktuellen Warenkorb als Parameter entgegen.
*   Anstatt die bestehende Liste zu verändern, wird eine *neue* Liste erstellt, die alle alten Elemente plus das neue Element enthält (mit dem Spread-Operator `...` in JavaScript oder `:+` in Scala).
*   Der Aufrufer ist dafür verantwortlich, die neue Liste zu speichern.

**1.4 - multiplyWithRandom (Pure Version – mit Einschränkung):**

Es ist nicht möglich, `multiplyWithRandom` in eine *echte* pure Funktion umzuwandeln, ohne die Zufälligkeit zu verlieren.  Eine pure Funktion muss bei gleichen Eingaben immer das gleiche Ergebnis liefern.  Wir können aber eine Technik namens "Dependency Injection" verwenden, um die Funktion testbarer zu machen:

```javascript
// JavaScript: Dependency Injection
function multiplyWith(number, randomValue) {
  return number * randomValue;
}

// Für den normalen Gebrauch:
console.log(multiplyWith(5, Math.random()));

// Für Tests (mit einem festen Wert):
console.log(multiplyWith(5, 0.5));  // Immer 2.5
```

```scala
// Scala: Dependency Injection
def multiplyWith(number: Double, randomValue: Double): Double = {
  number * randomValue
}

// Für den normalen Gebrauch:
println(multiplyWith(5, scala.util.Random.nextDouble()))

// Für Tests (mit einem festen Wert):
println(multiplyWith(5, 0.5)) // Immer 2.5
```

**Erklärung:**

*   Wir machen den Zufallswert zu einem expliziten Parameter.
*   Im Normalfall übergeben wir immer noch `Math.random()` / `Random.nextDouble()`.
*   Aber in Tests können wir einen festen Wert übergeben, um vorhersagbare Ergebnisse zu erhalten.  Das macht die *Logik* der Funktion testbar, auch wenn die Zufallsgenerierung selbst nicht pure ist.

**1.6 - printAndReturnString (Pure Version):**

```javascript
// JavaScript (wirklich pure)
function returnString(str) {
    return str;
}

// Wenn wir die Ausgabe *unbedingt* brauchen, aber getrennt halten wollen:
let result = returnString("Hello");
console.log(result);
```

```scala
// Scala (wirklich pure)
def returnString(str: String): String = {
  str
}

// Wenn wir die Ausgabe *unbedingt* brauchen, aber getrennt halten wollen:
val result = returnString("Hello")
println(result)
```

**Erklärung:**

*   Die pure Version gibt *nur* den String zurück.  Keine Ausgabe.
*   Wenn wir die Ausgabe an anderer Stelle *doch* brauchen, machen wir sie *außerhalb* der Funktion. So bleibt die Funktion selbst pure.

**Aufgabe 3 - Eigene Pure Functions (Rekursiv)**

Hier sind die rekursiven Implementierungen in Scala:

```scala
object RecursiveFunctions {

  // 3.1: Summe einer Liste von Zahlen
  def sumList(list: List[Int]): Int = list match {
    case Nil => 0 // Basisfall: Leere Liste, Summe ist 0
    case head :: tail => head + sumList(tail) // Rekursion: Kopf + Summe des Rests
  }

  // 3.2: Mittelwert einer Liste von Zahlen
  def averageList(list: List[Int]): Double = {
    if (list.isEmpty) 0.0 // Basisfall: Leere Liste
    else sumList(list).toDouble / list.length // Summe / Anzahl
    // Alternative mit innerer rekursiver Funktion für Tail-Rekursion:
    // (Nur nötig, wenn man mit sehr großen Listen rechnet)
    //  @scala.annotation.tailrec
    //  def averageHelper(remaining: List[Int], currentSum: Int, count: Int): Double = remaining match{
    //      case Nil => if(count==0) 0.0 else currentSum.toDouble / count
    //      case head :: tail => averageHelper(tail, currentSum+head, count+1)
    //  }
    // averageHelper(list, 0, 0)
  }


  // 3.3: Alphabetische Sortierung einer Liste von Strings
  def sortStrings(list: List[String]): List[String] = list match {
    case Nil => Nil // Basisfall: Leere Liste ist schon sortiert
    case head :: tail => insert(head, sortStrings(tail)) // Rekursion: Sortiere den Rest und füge den Kopf ein
  }

  // Hilfsfunktion für sortStrings: Fügt ein Element sortiert in eine Liste ein
  def insert(str: String, sortedList: List[String]): List[String] = sortedList match {
    case Nil => List(str) // Basisfall: In leere Liste einfügen
    case head :: tail =>
      if (str <= head) str :: sortedList // Einfügen, wenn str kleiner/gleich Kopf ist
      else head :: insert(str, tail) // Sonst rekursiv im Rest suchen
  }
  //3.4: Sortiere eine Liste nach Datum, Priorität und Titel
  case class Item(date: String, priority: Int, title: String)

    def sortByDatePriorityTitle(list: List[Item]): List[Item] = {
      list.sortWith { (a, b) =>
        if (a.date != b.date) a.date < b.date
        else if (a.priority != b.priority) a.priority < b.priority
        else a.title < b.title
      }
    }
// 3.5: Blätter aus einer Baumstruktur extrahieren

  sealed trait Tree[+A]
  case class Leaf[A](value: A) extends Tree[A]
  case class Branch[A](left: Tree[A], right: Tree[A]) extends Tree[A]

  def getLeaves[A](tree: Tree[A]): List[A] = tree match {
    case Leaf(value) => List(value) // Basisfall: Blatt gefunden
    case Branch(left, right) => getLeaves(left) ++ getLeaves(right) // Rekursion: Blätter aus beiden Ästen
  }

  def main(args: Array[String]): Unit = {
    // Beispiele
    val numbers = List(1, 2, 3, 4, 5)
    println(s"Summe: ${sumList(numbers)}") // Ausgabe: 15
    println(s"Mittelwert: ${averageList(numbers)}") // Ausgabe: 3.0

    val strings = List("banana", "apple", "orange")
    println(s"Sortiert: ${sortStrings(strings)}") // Ausgabe: List(apple, banana, orange)
      //Beispiele für Aufgabe 3.4
    val items = List(
      Item("2024-03-10", 2, "B"),
      Item("2024-03-08", 1, "C"),
      Item("2024-03-10", 1, "A")
    )

    val sortedItems = sortByDatePriorityTitle(items)
    println(sortedItems)  // List(Item(2024-03-08,1,C), Item(2024-03-10,1,A), Item(2024-03-10,2,B))

    // Beispiel für Aufgabe 3.5:
        val tree = Branch(
          Branch(Leaf("a"), Leaf("b")),
          Branch(Leaf("c"), Branch(Leaf("d"), Leaf("e")))
        )

        val leaves = getLeaves(tree)
        println(leaves)  // Ausgabe: List(a, b, c, d, e)
  }
}

```
