# Première étape

On définit une interface qui représente un élément.

CarElementVisitor.java
```java runnable
interface CarElement {
    void accept(CarElementVisitor visitor);
    // Méthode à définir par les classes implémentant CarElements
}
```

# Deuxième étape

On crée les classes qui étendent de cette interface.

Wheel.java
```java runnable
class Wheel implements CarElement {
    private String name;

    Wheel(String name) {
        this.name = name;
    }

    String getName() {
        return this.name;
    }

    public void accept(CarElementVisitor visitor) {
        visitor.visit(this);
    }
}
```

Engine.java
```java runnable
class Engine implements CarElement {
    public void accept(CarElementVisitor visitor) {
        visitor.visit(this);
    }
}
```

Body.java
```java runnable
class Body implements CarElement {
    public void accept(CarElementVisitor visitor) {
        visitor.visit(this);
    }
}
```

Car.java
```java runnable
class Car {
    CarElement[] elements;

    public CarElement[] getElements() {
        return elements.clone(); // Retourne une copie du tableau de références
    }

    public Car() {
        this.elements = new CarElement[] {
                new Wheel("front left"),
                new Wheel("front right"),
                new Wheel("back left"),
                new Wheel("back right"),
                new Body(),
                new Engine()
            };
    }
}
```

# Troisième étape

On crée une interface qui représente Visitor.

CarElementVisitor.java
```java runnable
interface CarElementVisitor {
    void visit(Wheel wheel);
    void visit(Engine engine);
    void visit(Body body);
    void visitCar(Car car);
}
```

# Quatrième étape

On crée deux classes visitor qui étendent l'interface précédente.

CarElementPrintVisitor.java
```java runnable
class CarElementPrintVisitor implements CarElementVisitor {
    public void visit(Wheel wheel) {
        System.out.println("Visiting "+ wheel.getName() + " wheel");
    }

    public void visit(Engine engine) {
        System.out.println("Visiting engine");
    }

    public void visit(Body body) {
        System.out.println("Visiting body");
    }

    public void visitCar(Car car) {
        System.out.println("\nVisiting car");
        for(CarElement element : car.getElements()) {
            element.accept(this);
        }
        System.out.println("Visited car");
    }
}
```

CarElementDoVisitor.java
```java runnable
class CarElementDoVisitor implements CarElementVisitor {
    public void visit(Wheel wheel) {
        System.out.println("Kicking my "+ wheel.getName());
    }

    public void visit(Engine engine) {
        System.out.println("Starting my engine");
    }

    public void visit(Body body) {
        System.out.println("Moving my body");
    }

    public void visitCar(Car car) {
        System.out.println("\nStarting my car");
        for(CarElement carElement : car.getElements()) {
            carElement.accept(this);
        }
        System.out.println("Started car");
    }
}
```

# Cinquième étape

On crée une classe de démonstration grâce aux deux classes précédentes.

TestVisitorDemo.java
```java runnable
public class TestVisitorDemo {
    static public void main(String[] args) {
        Car car = new Car();

        CarElementVisitor printVisitor = new CarElementPrintVisitor();
        CarElementVisitor doVisitor = new CarElementDoVisitor();

        printVisitor.visitCar(car);
        doVisitor.visitCar(car);
    }
}
```

# Sixième étape

On vérifie que tout cela fonctionne.

```java runnable
Visiting car
Visiting front left wheel
Visiting front right wheel
Visiting back left wheel
Visiting back right wheel
Visiting body
Visiting engine
Visited car

Starting my car
Kicking my front left
Kicking my front right
Kicking my back left
Kicking my back right
Moving my body
Starting my engine
Started car
```
