## Aufgabe 3 – TipCalculator

**Java - Imperativ (gegeben):**

```java
import java.util.ArrayList;
import java.util.List;

class TipCalculatorImperativ {
    private List<String> names = new ArrayList<>();
    private int tipPercentage = 0;

    public void addPerson(String name) {
        names.add(name);
        if(names.size() > 5) {
            tipPercentage = 20;
        } else if(names.size() > 0) {
            tipPercentage = 10;
        }
    }

    public List<String> getNames() {
        return names;
    }

    public int getTipPercentage() {
        return tipPercentage;
    }

    public static void main(String[] args) {
        TipCalculatorImperativ calculator = new TipCalculatorImperativ();
        System.out.println("Anfangs-Tip: " + calculator.getTipPercentage()); // 0
        calculator.addPerson("Alice");
        System.out.println("Tip nach Alice: " + calculator.getTipPercentage()); // 10
        calculator.addPerson("Bob");
        calculator.addPerson("Charlie");
        calculator.addPerson("David");
        calculator.addPerson("Eve");
        System.out.println("Tip nach 5 Personen: " + calculator.getTipPercentage()); // 10
        calculator.addPerson("Frank");
        System.out.println("Tip nach 6 Personen: " + calculator.getTipPercentage()); // 20
    }
}
```

**Scala - Imperativ (gegeben):**

```scala
import scala.collection.mutable.ListBuffer

class TipCalculatorImperativScala {
  private val names = ListBuffer[String]()
  private var tipPercentage = 0

  def addPerson(name: String): Unit = {
    names += name
    if (names.size > 5) {
      tipPercentage = 20
    } else if (names.nonEmpty) {
      tipPercentage = 10
    }
  }

  def getNames: List[String] = names.toList

  def getTipPercentage: Int = tipPercentage
}

object TipCalculatorImperativScalaApp extends App {
  val calculator = new TipCalculatorImperativScala()
  println(s"Anfangs-Tip: ${calculator.getTipPercentage}") // 0
  calculator.addPerson("Alice")
  println(s"Tip nach Alice: ${calculator.getTipPercentage}") // 10
  calculator.addPerson("Bob")
  calculator.addPerson("Charlie")
  calculator.addPerson("David")
  calculator.addPerson("Eve")
  println(s"Tip nach 5 Personen: ${calculator.getTipPercentage}") // 10
  calculator.addPerson("Frank")
  println(s"Tip nach 6 Personen: ${calculator.getTipPercentage}") // 20
}
```

**Java - Funktional ("pure Funktion"):**

```java
public class TipCalculatorFunktional {

    public static int getTipPercentage(int numberOfPeople) {
        if (numberOfPeople >= 1 && numberOfPeople <= 5) {
            return 10;
        } else if (numberOfPeople > 5) {
            return 20;
        } else {
            return 0; // Keine Gruppe = 0% Trinkgeld
        }
    }

    public static void main(String[] args) {
        System.out.println("Tip für 0 Personen: " + getTipPercentage(0)); // 0
        System.out.println("Tip für 1 Person: " + getTipPercentage(1)); // 10
        System.out.println("Tip für 5 Personen: " + getTipPercentage(5)); // 10
        System.out.println("Tip für 6 Personen: " + getTipPercentage(6)); // 20
    }
}
```

**Scala - Funktional ("pure Funktion"):**

```scala
object TipCalculatorFunktionalScala {
  def getTipPercentage(numberOfPeople: Int): Int = {
    numberOfPeople match {
      case n if n >= 1 && n <= 5 => 10
      case n if n > 5 => 20
      case _ => 0 // Keine Gruppe = 0% Trinkgeld
    }
  }

  def main(args: Array[String]): Unit = {
    println(s"Tip für 0 Personen: ${getTipPercentage(0)}") // 0
    println(s"Tip für 1 Person: ${getTipPercentage(1)}") // 10
    println(s"Tip für 5 Personen: ${getTipPercentage(5)}") // 10
    println(s"Tip für 6 Personen: ${getTipPercentage(6)}") // 20
  }
}
```

**Erläuterung zum funktionalen Ansatz (TipCalculator):**

*   Die Funktion `getTipPercentage` in der funktionalen Version nimmt die `numberOfPeople` direkt als Parameter entgegen.
*   Sie berechnet den Trinkgeldprozentsatz basierend auf dieser Eingabe und gibt ihn zurück.
*   Es gibt keinen internen Zustand, keine `names`-Liste oder `tipPercentage`-Variable als Instanzvariablen.
*   Die Funktion ist pure, da sie für die gleiche Eingabe immer den gleichen Output liefert und keine Seiteneffekte hat.
*   Die Logik ist klarer und direkter, da wir uns nur auf die Berechnung des Trinkgelds basierend auf der Gruppengröße konzentrieren.

**Zusammenfassend:**

Die funktionalen Lösungen sind in allen Beispielen deklarativer, kürzer und einfacher zu verstehen und zu testen, da sie den Fokus auf die Transformation von Daten legen, ohne sich um veränderlichen Zustand und Seiteneffekte kümmern zu müssen. Dies macht den Code robuster und wartungsfreundlicher.
