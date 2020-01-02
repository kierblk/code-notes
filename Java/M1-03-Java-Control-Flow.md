# Module 1: Java Control Flow

## What is the Output?

```Java
public class Tricky {
    public static void main(String[] args) {
        message1();
        message2();
        System.out.println("Done with main.");
    }

    public static void message1() {
        System.out.println("This is message1.");
    }

    public static void message2() {
        System.out.println("This is message2.");
        message1();
        System.out.println("Done with message2.");
    }
}
```

### Answer

```
This is message1.
This is message2.
This is message1.
Done with message2.
Done with main.
```

## What is the output?

```Java
public class Strange {
    public static void main(String[] args) {
        first();
        third();
        second();
        third();
    }

    public static void first() {
        System.out.println("Inside first method.");
    }

    public static void second() {
        System.out.println("Inside second method.");
        first();
    }

    public static void third() {
        System.out.println("Inside third method.");
        first();
        second();
    }
}
```

### Answer

```
Inside first method.
Inside third method.
Inside first method.
Inside second method.
Inside first method.
Inside second method.
Inside first method.
Inside third method.
Inside first method.
Inside second method.
Inside first method.
```

