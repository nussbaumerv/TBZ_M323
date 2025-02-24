## Aufgabe 1 - imperativ vs. deklarativ

**Java - Imperativ:**

```java
public class Aufgabe1Imperativ {

    public static int calculateScore(String word) {
        int score = 0;
        for (char c : word.toCharArray()) {
            if (c != 'a') {
                score++;
            }
        }
        return score;
    }

    public static void main(String[] args) {
        System.out.println("calculateScore(\"imperative\") == " + calculateScore("imperative")); // Erwartet: 9
        System.out.println("calculateScore(\"no\") == " + calculateScore("no")); // Erwartet: 2
        System.out.println("calculateScore(\"declarative\") == " + calculateScore("declarative")); // Erwartet: 9
        System.out.println("calculateScore(\"yes\") == " + calculateScore("yes")); // Erwartet: 3
    }
}
```

**Java - Deklarativ:**

```java
public class Aufgabe1Deklarativ {

    public static int wordScore(String word) {
        return (int) word.chars()
                .filter(c -> c != 'a') 
                .count();
    }

    public static void main(String[] args) {
        System.out.println("wordScore(\"imperative\") == " + wordScore("imperative")); // Erwartet: 9
        System.out.println("wordScore(\"no\") == " + wordScore("no")); // Erwartet: 2
        System.out.println("wordScore(\"declarative\") == " + wordScore("declarative")); // Erwartet: 9
        System.out.println("wordScore(\"yes\") == " + wordScore("yes")); // Erwartet: 3
    }
}
```

**Scala - Imperativ:**

```scala
object Aufgabe1ImperativScala {
  def calculateScore(word: String): Int = {
    var score = 0
    for (c <- word) {
      if (c != 'a') { 
        score += 1
      }
    }
    score
  }

  def main(args: Array[String]): Unit = {
    println(s"""calculateScore("imperative") == ${calculateScore("imperative")}""") // Erwartet: 9
    println(s"""calculateScore("no") == ${calculateScore("no")}""") // Erwartet: 2
    println(s"""calculateScore("declarative") == ${calculateScore("declarative")}""") // Erwartet: 9
    println(s"""calculateScore("yes") == ${calculateScore("yes")}""") // Erwartet: 3
  }
}
```

**Scala - Deklarativ:**

```scala
object Aufgabe1DeklarativScala {
  def wordScore(word: String): Int = {
    word.count(_ != 'a') 
  }

  def main(args: Array[String]): Unit = {
    println(s"""wordScore("imperative") == ${wordScore("imperative")}""") // Erwartet: 9
    println(s"""wordScore("no") == ${wordScore("no")}""") // Erwartet: 2
    println(s"""wordScore("declarative") == ${wordScore("declarative")}""") // Erwartet: 9
    println(s"""wordScore("yes") == ${wordScore("yes")}""") // Erwartet: 3
  }
}
```

**Erläuterung:**

*   **Imperativ:** Wir iterieren explizit über jedes Zeichen des Wortes und erhöhen den `score` nur, wenn das Zeichen nicht 'a' ist.
*   **Deklarativ:** Wir verwenden `chars().filter().count()` in Java Streams bzw. `word.count(_ != 'a')` in Scala, um die Zeichen zu filtern und direkt zu zählen, ohne explizite Schleifen. Die deklarative Lösung ist kürzer, lesbarer und fokussiert sich darauf, *was* berechnet werden soll (Anzahl Zeichen ungleich 'a'), nicht *wie* es berechnet wird.

