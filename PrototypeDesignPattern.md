# Prototype Design Pattern
### Creational design pattern used to let you copy/clone existing objects, without making your code dependent on thier class
- The pattern declares a **common interface** for all objects that support cloning.
- This interface lets you clone an object without coupling your code to the class of that object.
- Usually, such an interface contains just a single **clone** method.

#### The Prototype interface declares the cloning methods. In most cases, it’s a single clone method.
1. The Prototype interface declares the cloning methods. In most cases, it’s a **single clone method**.
2. The Concrete Prototype class implements the cloning method. In addition to copying the original object’s data to the clone, this method may also handle some edge cases of the cloning process related to cloning linked objects, untangling recursive dependencies, etc.
3. The Client can produce a copy of any object that follows the prototype interface.

#### Original Protype Interface

```
public interface Prototype {
    Prototype clone();
}
```
#### Concrete class
```
class ConcretePrototype implements Prototype {
    private String name;
    private int value;

    // Constructor
    public ConcretePrototype(String name, int value) {
        this.name = name;
        this.value = value;
    }

    // Getters and setters
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getValue() {
        return value;
    }

    public void setValue(int value) {
        this.value = value;
    }

    // Override clone() method
    @Override
    public ConcretePrototype clone() {
        try {
            // Shallow copy
            return (ConcretePrototype) super.clone();
        } catch (CloneNotSupportedException e) {
            throw new RuntimeException("Clone not supported", e);
        }
    }

    @Override
    public String toString() {
        return "ConcretePrototype{name='" + name + "', value=" + value + "}";
    }
}

```
#### Client Code
````
public class PrototypeDemo {
    public static void main(String[] args) {
        // Create an original object
        ConcretePrototype original = new ConcretePrototype("Original", 42);

        // Clone the original object
        ConcretePrototype cloned = original.clone();

        // Modify the cloned object
        cloned.setName("Cloned");
        cloned.setValue(100);

        // Print both objects to show they're independent
        System.out.println("Original Object: " + original);
        System.out.println("Cloned Object: " + cloned);
    }
}

````


