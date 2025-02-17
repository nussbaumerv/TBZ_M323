## Aufgabe 2 - Umsetzung einer Shopping Cart Funktion

**Erster Schritt: Imperativ ("falsch") - Java**

```java
import java.util.ArrayList;
import java.util.List;

public class ShoppingCartImperativ {
    private List<String> items = new ArrayList<>();
    private boolean bookAdded = false;

    public void addItem(String item) {
        items.add(item);
        if (item.toLowerCase().contains("buch")) {
            bookAdded = true;
        }
    }

    public void removeItem(String item) {
        items.remove(item);
        if (item.toLowerCase().contains("buch")) { 
            if (!containsBook()) {
                bookAdded = false;
            }
        }
    }

    private boolean containsBook() {
        for (String item : items) {
            if (item.toLowerCase().contains("buch")) {
                return true;
            }
        }
        return false;
    }


    public List<String> getItems() {
        return new ArrayList<>(items); 
    }

    public double getDiscountPercentage() {
        return bookAdded ? 0.05 : 0.0;
    }

    public static void main(String[] args) {
        ShoppingCartImperativ cart = new ShoppingCartImperativ();
        cart.addItem("T-Shirt");
        System.out.println("Warenkorb: " + cart.getItems() + ", Rabatt: " + cart.getDiscountPercentage()); // Rabatt: 0.0
        cart.addItem("Harry Potter Buch");
        System.out.println("Warenkorb: " + cart.getItems() + ", Rabatt: " + cart.getDiscountPercentage()); // Rabatt: 0.05
        cart.removeItem("Harry Potter Buch");
        System.out.println("Warenkorb: " + cart.getItems() + ", Rabatt: " + cart.getDiscountPercentage()); // Rabatt: 0.05 (Problem!)
        cart.addItem("Tolkien Buch");
        System.out.println("Warenkorb: " + cart.getItems() + ", Rabatt: " + cart.getDiscountPercentage()); // Rabatt: 0.05
        cart.removeItem("Tolkien Buch");
        System.out.println("Warenkorb: " + cart.getItems() + ", Rabatt: " + cart.getDiscountPercentage()); // Rabatt: 0.0 (behoben durch containsBook())
    }
}
```

**Erster Schritt: Imperativ ("falsch") - Scala**

```scala
import scala.collection.mutable.ListBuffer

class ShoppingCartImperativScala {
  private val items = ListBuffer[String]()
  private var bookAdded = false

  def addItem(item: String): Unit = {
    items += item
    if (item.toLowerCase.contains("buch")) {
      bookAdded = true
    }
  }

  def removeItem(item: String): Unit = {
    items -= item
    if (item.toLowerCase.contains("buch")) {
      if (!containsBook) {
        bookAdded = false
      }
    }
  }

  private def containsBook: Boolean = {
    items.exists(_.toLowerCase.contains("buch"))
  }

  def getItems: List[String] = items.toList

  def getDiscountPercentage: Double = if (bookAdded) 0.05 else 0.0
}

object ShoppingCartImperativScalaApp extends App {
  val cart = new ShoppingCartImperativScala()
  cart.addItem("T-Shirt")
  println(s"Warenkorb: ${cart.getItems}, Rabatt: ${cart.getDiscountPercentage}") // Rabatt: 0.0
  cart.addItem("Harry Potter Buch")
  println(s"Warenkorb: ${cart.getItems}, Rabatt: ${cart.getDiscountPercentage}") // Rabatt: 0.05
  cart.removeItem("Harry Potter Buch")
  println(s"Warenkorb: ${cart.getItems}, Rabatt: ${cart.getDiscountPercentage}") // Rabatt: 0.05 (Problem!)
  cart.addItem("Tolkien Buch")
  println(s"Warenkorb: ${cart.getItems}, Rabatt: ${cart.getDiscountPercentage}") // Rabatt: 0.05
  cart.removeItem("Tolkien Buch")
  println(s"Warenkorb: ${cart.getItems}, Rabatt: ${cart.getDiscountPercentage}") // Rabatt: 0.0 (behoben durch containsBook())
}
```

**Hinweis zum imperativen Ansatz:**

*   Der Zustand des Warenkorbs (`items`, `bookAdded`) wird innerhalb der Klasse verwaltet und durch Methodenaufrufe verändert.
*   Das Problem bei `removeItem` und `bookAdded` zeigt, wie Zustandsänderungen komplex werden können und Fehleranfällig sind, insbesondere wenn mehrere Zustandsvariablen voneinander abhängen. Wir mussten `containsBook()` hinzufügen, um das Problem zu beheben, was die Komplexität weiter erhöht.

**Zweiter Schritt: Funktional ("richtig") - Java**

```java
import java.util.List;

public class ShoppingCartFunktional {

    public static double getDiscountPercentage(List<String> shoppingCart) {
        boolean containsBook = false;
        for (String item : shoppingCart) {
            if (item.toLowerCase().contains("buch")) {
                containsBook = true;
                break;
        }
        return containsBook ? 0.05 : 0.0;
    }

    public static void main(String[] args) {
        List<String> cart1 = List.of("T-Shirt", "Hose");
        System.out.println("Warenkorb: " + cart1 + ", Rabatt: " + getDiscountPercentage(cart1)); // Rabatt: 0.0
        List<String> cart2 = List.of("T-Shirt", "Harry Potter Buch");
        System.out.println("Warenkorb: " + cart2 + ", Rabatt: " + getDiscountPercentage(cart2)); // Rabatt: 0.05
        List<String> cart3 = List.of("T-Shirt", "Socken");
        System.out.println("Warenkorb: " + cart3 + ", Rabatt: " + getDiscountPercentage(cart3)); // Rabatt: 0.0
    }
}
```

**Zweiter Schritt: Funktional ("richtig") - Scala**

```scala
object ShoppingCartFunktionalScala {
  def getDiscountPercentage(shoppingCart: List[String]): Double = {
    if (shoppingCart.exists(_.toLowerCase.contains("buch"))) 0.05 else 0.0
  }

  def main(args: Array[String]): Unit = {
    val cart1 = List("T-Shirt", "Hose")
    println(s"Warenkorb: $cart1, Rabatt: ${getDiscountPercentage(cart1)}") // Rabatt: 0.0
    val cart2 = List("T-Shirt", "Harry Potter Buch")
    println(s"Warenkorb: $cart2, Rabatt: ${getDiscountPercentage(cart2)}") // Rabatt: 0.05
    val cart3 = List("T-Shirt", "Socken")
    println(s"Warenkorb: $cart3, Rabatt: ${getDiscountPercentage(cart3)}") // Rabatt: 0.0
  }
}
```

**Erläuterung zum funktionalen Ansatz:**

*   Die Funktion `getDiscountPercentage` ist eine *pure Funktion*. Sie nimmt eine Liste von Strings (den Warenkorb) als Eingabe und gibt den Rabattprozentsatz als Ausgabe zurück.
*   Sie hat keine Seiteneffekte. Sie ändert keinen Zustand außerhalb der Funktion und hängt nur von der Eingabe ab.
*   Die Logik ist klarer und einfacher zu testen, da wir uns keine Gedanken über den internen Zustand eines Objekts machen müssen.
*   Wir verwenden `exists` in Scala (oder eine ähnliche Logik in Java), um deklarativ zu prüfen, ob ein Buch im Warenkorb vorhanden ist.