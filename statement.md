# Première étape

Définir une interface qui représente un élément.

CarElementVisitor.java
```java runnable
// { autofold

interface CarElement {
    void accept(CarElementVisitor visitor);
    // Méthode à définir par les classes implémentant CarElements
}
// }
```

# Deuxième étape

Créer les classes qui étendent de cette interface.

Wheel.java
```java runnable
// { autofold
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
// }
```

Engine.java
```java runnable
// { autofold
class Engine implements CarElement {
    public void accept(CarElementVisitor visitor) {
        visitor.visit(this);
    }
}
// }
```

Body.java
```java runnable
// { autofold
class Body implements CarElement {
    public void accept(CarElementVisitor visitor) {
        visitor.visit(this);
    }
}
// }
```
