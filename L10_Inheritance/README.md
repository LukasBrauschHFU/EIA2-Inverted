# L10_Inheritance

![](Material/Evolution.jpg)

## Generalisierung vs Spezialisierung
<img src="Material/barabara-liskov.jpg" width="100" align="right"/>

1987 stellte Bararbara Liskov auf einer Konferenz einen Kerngedanken der objektorientierten Modellierung vor. Danach soll ein Objekt einer Klasse durch ein Objekt einer Sub-Klasse dieser Klasse ersetzt werden können, ohne dass das Programm, welches das Objekt verwendet, verändert werden muss. 1993 formalisierte sie zusammen mit Jeannette Wing was heute als das **Liskov'sche Substitutionsprinzip** bekannt ist.

Bezogen auf Hunde kann das Liskov'sche Substitutionsprinzip folgendermaßen beispielhaft dargestellt werden:  
Wenn Hunde grundsätzlich bellen können, dann können auch Subklassen von `Hund`, wie `Dogge`, `Chihuahua` und `Pudel` bellen. Wenn Du also an einem Haus klingelst, an dem ein Schild "Warnung vor dem Hund" steht, darfst Du davon ausgehen, dass ein Hund bellen wird. Es ist nicht erforderlich, dass auf dem Schild "Warnung vor dem Pudel" steht, auch wenn der Hund in dem Haus ein Pudel sein sollte.  

`Pudel` ist eine Spezialisierung von `Hund`, `Hund` ist die Generalisierung von `Pudel`.  

Pudel gelten als besonders gelehrig und werden daher gerne für besondere Tricks und im Zirkus eingesetzt. Dabei ist es wiederum unerheblich, ob es sich um Toy-, Zwerg-, oder Großpudel handelt. Diese sind Spezialisierungen von Pudel, die sich in der Varianz der Größe unterscheiden.  

Der `Hund` kann weiter generalisiert werden, denn er gehört zu der Familie der `Hundeartigen`, zu denen beispielsweise auch Bären, Robben und Stinktiere gehören. Zusammen mit den `Katzenartigen` stellen die `Hundeartigen` die `Raubtiere` die wiederum zu der Klasse der `Säugetiere` gehören, von denen auch der `Mensch` eine Spezialisierung darstellt.  

## Darstellung im Klassendiagramm
In der Biologie teilt man ein in Klassen, Rassen, Arten, Gattungen, Familien, Ordnungen und so weiter. Bei der objektorientierten Modellierung muss man lediglich Klassen unterscheiden in Super- und Subklassen. 

Die Superklasse stellt die Generalisierung einer Subklasse dar, die Subklasse eine Spezialisierung der Superklasse.

Im Klassendiagramm verweisen Pfeile mit einer dreieckigen und leeren Spitze von der Subklasse auf ihre Superklasse und stellen so diese Beziehung dar. Der oben angeführte Exkurs in die Biologie, der übrigens keiner wissenschaftlichen Überprüfung standhält, könnte im Klassendiagramm folgendermaßen aussehen.  

![](Material/draw.io/Dogs_ClassDiagram.svg)

- [x] Studiere das Diagramm und mache dir die Beziehung zwischen Sub- und Superklasse klar.
- [x] Beschreibe nur anhand des Diagramms die Eigenschaften und Fähigkeiten eines Zwergpudels.
- [x] Sollten die verschiedenen Pudel eigene Subklassen bilden? Was wäre eine Alternative?
- [x] Wie hilft dir ein solches Diagramm und die Betrachtung von Generalisierung und Spezialisierung im Umgang mit Lebewesen? Beschreibe es an diesem Beispiel. 

## Vererbung
In diesem Zusammenhang spricht man auch von Vererbung (Inheritance). Eine Superklasse vererbt alle ihre Eigenschaften und Methoden an die Subklasse, so wie es bei obigem Stammbaum der Arten gezeigt ist.

> **Vererbung** ist das dritte Prinzip der Objektorientierung!

Wegen der Vererbungsbeziehung werden Superklassen manchmal auch als Elternklassen und Subklassen als Kindklassen bezeichnet. Das führt aber zur Verwirrung, da die manche Laufzeitbeziehungen zwischen Objekten, beispielsweise im DOM, bereits als Parent-Child-Beziehung bezeichnet wird. Weitere Begriffe sind Ober- und Unterklasse, Basis- und Abgeleitete Klasse und weitere. In dieser Lektion werden weiter strikt die Bezeichnungen Super- und Subklasse genutzt.

## Regeln für die Modellierung
Ein Dompteur im Zirkus muss nicht nur die Eigenheiten jeder Hunderasse in seiner Truppe kennen, sondern sogar die jeder einzelnen Instanz. Dem Schalterbeamten "in Zollhafe von modernes Planet" genügte dagegen zu wissen, ob eine Lebensform ein Säuger ist, um das richtige Zimmer zuzuweisen ([siehe Ijon Tichy, Folge 2, 4:23 - 5:33](https://www.youtube.com/watch?v=_DSCXsIR03Q))

Bei der Modellierung eines Systems solltes Du diese zwei Regeln beachten:
- jeder Teil darf nur so schlau wie nötig sein
- jeder Teil muss so dumm wie möglich sein  

Jeder Teil soll also nur das von seiner Umwelt und anderen Teilen wissen, was unbedingt erforderlich für die eigene Funktion ist!

# Ufos in Asteroids

Unter Berücksichtigung der oben genannten Prinzipien wird Asteroids weiter entwickelt.

**Video: Erweiterung des Klassendiagramms**
- weitere Objekttypen sind Ufo, Schiff, Projektile, Laser und Trefferzone
- Ufo und Projektile sind den Asteroiden nicht unähnlich
  - haben einige Gemeinsamkeiten aber anderes Aussehen und andere Bewegungsmethode
  - werden zuerst modelliert
- Gemeinsamkeiten werden in Superklasse verlagert und von dort vererbt
  - Name? Body, Moveable, Thing
- Asteroid wird als Spezialisierung definiert
- Ufos haben anderes Bewegungsmuster und festgelegte Geschwindigkeit
- Projektile haben gleiches Bewegungsmuster aber Reichweite und festgelegte Geschwindigkeit
- Aktivitätsdiagramme für Moveable und Asteroids vorzeigen und erklären, nicht neu entwerfen

**Video: Implementation I von Moveable, Refaktorierung von Asteroid und Tests**   
- Asteroids und Moveable aufteilen
- Testen
- extends erklären!
- super(...) erklären!

- Projektilklasse implementieren und testen
  - wie Reichweite implementieren?
    - range in Projectile, wird dezimiert
    - was passiert wenn 0 unterschritten wird?
      - zunächst velocity auf (0,0)
    - aber Projektile müssen gelöscht werden
  - Zudem: derzeit nur eines, referenziert durch eine Variable
    - es soll aber viele geben
    - weitere Liste für Projektile?
    - dann noch eine für Ufos?
    - das ist doof, zumal das Hauptprogramm mit allen das gleiche macht....
    
> **`extends`** erweitert eine Superklasse um eine Subklasse!  
> **`super(...)`** ruft aus der Subklasse den Constructor der Superklasse auf!  
> **`super.methode(...)`** ruft aus der Subklasse die `methode` der Superklasse auf!

## Polymorphie

Griechisch πολύς (polýs) = „viel“ und μορφή (morphé) = "Form, Gestalt". Hunde sind vielgestaltig, das wurde in diesen Lektionen bereits ausgiebig behandelt. Die einzelnen Hunderassen können aber nicht nur anders aussehen, sondern sich vielleicht auch unterschiedlich verhalten. Ein Jagdhund wird beim Anblick einer Herde Schafe vielleicht gerne hineinrennen und eines reißen, ein Hütehund eher um die Herde herumlaufen und sie beisammen halten. Für jemanden, der mit diesen Hunden spazierengeht, so wie die angeblich 200.000 professionellen Gassigeher in den USA, ist dabei vordringlich wichtig, genug Leinen und Halsbänder zu haben, um die Hunde bei sich halten zu können. Die Rasse ist nicht erheblich.

> **Polymorphie** ist das vierte Prinzip der Objektorientierung!

Im Asteroids-Programm sind derzeit zwei Klassen implementiert, die von Moveable erben, also zwei Subklassen der Superklasse Moveable. Anders ausgedrückt hat Moveable derzeit drei Gestalten: Moveable, Asteroid und Projectile. Sie unterscheiden sich in Aussehen und Verhalten

| Klasse | Aussehen | Bewegung |
|---|---|---|
|Moveable|keines|Geradlinig mit Umlauf am Rand
|Asteroid|Felsbrocken| wie Moveable
|Projectile| kleiner Punkt| wie Moveable aber Reichweite begrenzt

Damit sich die Instanzen der Klassen bewegen und darstellen können, ruft das Hauptprogramm deren `move`- und `draw`-Methoden auf. Dabei ist es dem Hauptprogramm aber völlig egal, ob es sich dabei um Asteroiden oder Projektile handelt, solange sie Moveables sind und somit diese Methoden entweder geerbt haben oder sie neu implementieren (überschreiben). Das Hauptprogramm kann mit allen Gassi gehen ...

Nach dem Liskov'schen Substitutionsprinzip muss Folgendes möglich sein, auch wenn Moveable vielgestaltig ist:

```typescript
let m: Moveable = new Moveable();
let a: Moveable = new Asteroid(1);
let p: Moveable = new Projectile(new Vector(0, 0), new Vector(0, 0));
```

Beachte, dass die Variablen m, a und p alle mit dem Typ Moveable deklariert wurden, sie aber unterschiedliche Objekt-Typen referenzieren.

- [x] Implementiere diese drei Zeilen und lasse dir die Variablen in der Konsole ausgeben oder schaue sie dir im Debugger an.

Wenn Vorangegangenes möglich ist, dann muss auch Folgendes möglich sein:

```typescript
let moveables: Moveable[] = [];
moveables.push(new Asteroid(1));
moveables.push(new Projectile(new Vector(0, 0), new Vector(0, 0)));
```

- [x] Überprüfe auch dies mit einer entsprechenden Implementation


**Video: Aktivitätsdigramm Hauptprogramm**  
Bild/Scan: Aktivitätsdiagramm des Hauptprogramms mit asteroid/asteroids ersetzt durch moveable/moveables

## Implementation II

**Video: Implementation II (Nutzung der Polymorphie)**
- asteroids -> moveables, Type Asteroid -> Moveable
- asteroid to moveable in Loops
- moveable instance of Asteroid in getAsteroidHit
- einzelne projectile-Variable eliminieren
  - stattdessen Projektile in moveables pushen
  - Sonderbehandlung in Update eliminieren
- geht alles recht schnell
- aber Projektile bleiben auf Canvas kleben
  - einfache, schnelle Lösung:
    - moveables exportieren, Projektile finden und löschen sich selbst.
  - damit aber werden die Projectile zu mächtig
    - eleganter: als expendable markieren und Hauptprogramm löscht sie -> Verweis auf Garbage-Collector für später
- expendable auch auf Asteroiden nach Break anwenden

> **`a instanceof B`** prüft, ob das Objekt `a` eine Instanz der Klasse `B` ist.

- [x] Implementiere die Ufos! Dabei musst Du unter anderem folgende Designentscheidung treffen:
  - wer soll die Projektile erzeugen? Wird diese Aufgabe von den Ufos übernommen oder vom Hauptprogramm?
    - wenn Ufo: wie kommen die Projektile in das Moveable-Array um verwaltet zu werden?
    - wenn Hauptprogramm: wie erkennt das Hauptprogramm, dass das Ufo ein Projektil abfeuert? 

Der Pfad wird bereits von der Funktion `createUfoPath()` erzeugt. 