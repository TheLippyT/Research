Java SE 11 Programmer 2

## Java SE 11 Programmer II

- [Java Fundamentals](#Java-Fundamentals)
- [Annotations](#Annotations)
- [Generics and Collections](#Generics-and-Collections)
- [Functional Programming](#Functional-Programming)
- [Exceptions, Assertions, and Localization](#Exceptions-Assertions-and-Localization)
- [Modular Applications](#Modular-Applications)
- [Concurrency](#Concurrency)
- [I/O](#I/O)
- [NIO.2](#NIO.2)
- [JDBC](#JDBC)
- [Security](#Security)

### Java Fundamentals

1.  A final variable does not need to be assigned when it is declared, only before it is used. A variable reference being marked as final does not mean the associated object cannot be modified. If an instance variable is final, then it must be assigned a value when it is declared or when the object is instantiated. Similarly, static variables must be assigned a value when declared or in a static initialiser.
    
2.  Methods marked final cannot be overridden by a subclass. This essentially prevents any polymorphic behaviour on the method call and ensures that a specific version of the method is always called. The opposite of a final method is an abstract method as an abstract method must be implemented.
    
3.  A final class cannot be extended. A class cannot be both abstract and final.
    
4.  An enum can be used to specify a fixed set of constants. Using an enum is better than using constants because it provides type-safe checking. Another advantage of an enum is the enum value can be used in a switch statement. An enum can contain methods but the first line must be the list of values. Note that if an enum has a body (e.g. default value) then the semicolon becomes mandatory.
    
    ```java
    public enum Season{
        WINTER, SPRING, SUMMER, FALL
    }
    ```
    
5.  A nested class is one that is defined within another class. There are 4 types:
    
    - **Inner class:** A non-static type defined at the member level.
    - **Static nested class:** A static typed defined at the member level.
    - **Local class:** A class defined within a method body.
    - **Anonymous class:** A special case of a local class that does not have a name.
6.  An inner class cannot declare static fields or methods, except for static final fields. It can also access members of the outer class including private methods. An inner classes will result in an Outer$Inner.class file being created by the compiler. As inner class can have the same variable names as outer classes, a call to **this** is prefixed with the class name.
    
7.  A static nested class can be instantiated without an instance of the enclosing class. However, it can not access the instance variables or methods in the outer class directly. It requires an explicit reference to the outer class variable. The nesting creates a namespace because the enclosing class name must be used to refer to it.
    
8.  A local class is declared in a method, constructor or initialiser. A local class does not have any access modifiers and cannot be declared static or declare static fields unless they are static final. When defined in an instance method, they have access to all fields and methods of the enclosing class. They can access local variables only if the variables are final or effectively final. An effectively final variable is one whose value does not change after it is set.
    
9.  An anonymous class is a special form of a local class that does not have a name. It is declared and instantiated in one statement using the new keyword, a type name with parentheses, and a set of braces. Anonymous classes are required to extend an existing class or implement an existing interface.
    
10. The rules for modifiers in nested classes are summarised below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table1.1.JPG)![table1.1.jpg](../_resources/e2ead8e099954cf793b1b0481364d127.jpg)
    
11. The rules for members in nested classes are summarised below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table1.2.JPG)![table1.2.jpg](../_resources/bb6f13dfbfd2459cb1f52b3c8e55b9ae.jpg)
    
12. The rules for access in nested classes are summarised below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table1.3.JPG)![table1.3.jpg](../_resources/37dc74492d3a4e4f9dca0e6a55bdb758.jpg)
    
13. When Java was first released, there were only two types of members an interface declaration could include: abstract methods and static final variables. Since Java 8 and 9, new method types have been added. The interface member types are summarised below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table1.4.JPG)![table1.4.jpg](../_resources/56c62e51dd014212b9222c034d6e07dc.jpg)
    
14. A default method may be declared within an interface to provide a default implementation. The default method is assumed to be public and cannot be marked abstract, final, or static. It may also be overridden by a class that implements the interface. If a class inherits two or more default methods with the same method signature, then the class must override the method.
    
15. To call a default method from a class which overrides the implementation:
    
    ```java
    interfaceName.super.methodName();
    ```
    
16. A static interface method must include a method body and is assumed to be public. It cannot be marked abstract or final and cannot be referenced without using the interface name. Static interface methods are not inherited by a class implementing the interface.
    
17. A private interface method is used to avoid code duplication in instance methods. It must be marked private and include a method body. It may only be called by default and private (non-static) methods within the interface definition.
    
18. A private static method is used to avoid code duplication in static methods. It must be marked private and static and may only be called by other methods within the interface definition.
    
19. The rules for interface member access are summarised below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table1.5.JPG)![table1.5.JPG](../_resources/26a0358f4b7c4a3eb7c79dc83e659204.JPG)
    
20. A functional interface is an interface that contains a single abstract method. A lambda expression is like an anonymous class that defines one method. Any functional interface can be implemented as a lambda expression.
    
21. Note that if a functional method includes an abstract method with the same signature as a public method found in Object, then those methods do not count towards the single abstract method test. This includes:
    
    ```java
    String toString()
    boolean equals(Object)
    int hashCode()
    ```
    
22. A lambda expression contains a parameter name, arrow, and body. The parameters list the variables, which must be compatible with the type and number of input parameters of the functional interface's single abstract method. The body must also be compatible with the return type of the functional interface's abstract method. Example lambda expressions are shown below:
    
    ```java
    a -> a.canHop()
    (Animal a) -> {return a.canHop();}
    ```
    
23. A var parameter can be used in the parameter list, but then all parameters must use var. If the type is specified for one parameter, then it must be specified for all parameters. A semicolon is mandatory in the body if there is only a single expression. An expression-based lambda body is not terminated with a semicolon as it is an expression not a statement. However, a statement-based lambda with multiple lines requires that each statement be terminated with a semicolon.
    

### Annotations

1.  Annotations are all about metadata. They let you assign metadata attributes to classes, methods, variables, and other Java types. An example is shown below:
    
    ```java
    public class Mammal{}
    public class Bird{}
    
    @ZooAnimal public class Lion extends Mammal{}
    @ZooAnimal public class Peacock extends Bird{}
    ```
    
2.  The above could have been achieved by extending a ZooAnimal class but that would require the class hierarchy to be changed. Annotations are like interfaces. While interface can be applied to classes, annotations can be applied to classes, methods, expressions, and even other annotations. Annotations also allow a set of values to be passed. An example is shown below:
    
    ```java
    public class Veterinarian{
        @ZooAnimal(habitat="Infirmary") private Lion sickLion;
        @ZooAnimal(habitat="Safari") private Lion healthyLion;
        @ZooAnimal(habitat="Special Enclosure") private Lion blindLion;
    }
    ```
    
3.  The values are part of the type declaration and not of the variable. Without annotations, a new Lion type for each habitat value would need to be defined. This would become difficult in large applications.
    
4.  To declare an an annotation the @interface annotation is used. An example is shown below:
    
    ```java
    public @interface Exercise{}
    }
    ```
    
5.  To apply the annotation to other code we simply use the @Exercise annotation. A parenthesis is required if there are elements specified, and optional otherwise. Examples are shown below:
    
    ```java
    @Exercise() public class Cheetah{}
    @Exercise public class Sloth{}
    @Exercise
    public class ZooEmployee{}
    ```
    
6.  To declare an annotation with elements the elements need to be available in the annotation declaration. An example is shown below:
    
    ```java
    public @interface Exercise{}
        int hoursPerDay();
    }
    ```
    
7.  This changes how the annotation is used. An example is shown below:
    
    ```java
    @Exercise(hoursPerDay=3) public class Cheetah{}
    ```
    
8.  When declaring an annotation, any element without a default value is considered required. A default value must be a non-null constant expression. An example including a default value is shown below:
    
    ```java
    public @interface Exercise{}
        int hoursPerDay();
        int startHour() default 6;
    }
    ```
    
9.  The element type must be a primitive type, a String, a Class, an enum, another annotation, or an array of any of these types. Note that this excludes wrapper classes and arrays of arrays.
    
10. Like abstract interface methods, annotation elements are implicitly abstract and public. Declaring elements protected, private or final will result in a compilation failure.
    
11. Like interface variables, annotation variables are implicitly public, static, and final. A constant variable can be declared in an annotation but are not considered elements.
    
12. A shorthand format exists for using annotations. This can occur if the annotation declaration contains an element named *value()*, the usage of the annotation provides no values for other elements, and the declaration does not contain any elements that are required. An example is shown below:
    
    ```java
    public @interface Injured{
        String veterinarian() default "unassigned";
        String value() default "foot";
        int age() default 1;
    }
    
    @Injured("Legs") public void fallDown() {}
    ```
    
13. A shorthand format also exists for providing an array that contains a single element. An example is shown below:
    
    ```java
    public @interface Music{
        String[] genres();
    }
    
    public class Giraffe{
        @Music(genres={"Rock and roll"}) String mostDisliked;
        @Music(genres="Classical") String favorite;
    }
    ```
    
14. An annotation can be applied to an annotation to specify what types the annotation can be applied to. This is done by specifying the ElementType using @Target. An example is shown below:
    
    ```java
    @Target({ElementType.METHOD,ElementType.CONSTRUCTOR})
    public @interface ZooAttraction{}
    ```
    
15. The options for ElementType are shown below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table2.1.JPG)![table2.1.JPG](../_resources/5b8bf92838b14920b40e04a21f8d560b.JPG)
    
16. The TYPE\_USE value covers nearly all other values. One exception is that it can only be used on a method that returns a value, a void method would still need METHOD defined in the annotation. TYPE\_USE is typically used for cast operations, object creation with new and inside type declarations.
    
17. The compiler discards certain types of information when converting source code into a .class file. Annotations may be discarded by the compiler at runtime. The @Retention annotation can be used to specify. The options for @Retention are shown below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table2.2.JPG)![table2.2.JPG](../_resources/2fb458b3f669410e8bbd749a62b62d1e.JPG)
    
18. Javadoc is a built-in standard within Java that generates documentation for a class or API. If the @Documented annotation is present, then the generated Javadoc will include annotation information defined on Java types. An example is shown below:
    
    ```java
    // Hunter.java
    import java.lang.annotation.Documented;
    @Documented public @interface Hunter{}
    
    // Lion.java
    @Hunter public class Lion{}
    ```
    
19. In the above example @Hunter would be published with the Lion Javadoc information because it is marked with @Documented.
    
20. The @Inherited annotation is used to allow subclasses to inherit the annotation information found in the parent class.
    
    ```java
    // Vertebrate.java
    import java.lang.annotation.Inherited;
    @Inherited public @interface Vertebrate{}
    
    // Mammal.java
    @Vertebrate public class Mammal{}
    
    // Dolphin.java
    public class Dolphin extends Mammal{}
    ```
    
21. In the above example the @Vertebrate annotation will be applied to both Mammal and Dolphin.
    
22. The @Repeatable annotation can be used to apply an annotation more than once. To declare a @Repeatable annotation, a containing annotation with type value must be defined.
    
    ```java
    // Containing annotation type
    public @interface Risks{
        Risk[] value();
    }
    
    // Containing annotation class
    @Repeatable(Risks.class)
    public @interface Risk{
        String danger();
        int level() default 1;
    }
    
    public class Zoo{
        public static class Monkey{}
        @Risk(danger="Silly")
        @Risk(danger="Aggressive",level=5)
        @Risk(danger="Violent",level=10)
        private Monkey monkey;
    }
    ```
    
23. Commonly used built-in annotations are shown below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table2.5.JPG)![table2.5.JPG](../_resources/63264ce6f78f465c8c55de81b07c0971.JPG)
    
24. Example applications of commonly used annotations are shown below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table2.6.JPG)![table2.6.jpg](../_resources/11e26fb3bf354f9f870942514bc19c1e.jpg)
    

### Generics and Collections

1.  Method references can make code easier to read. An example is shown below:
    
    ```java
    @FunctionalInterface
    public interface LearnToSpeak{
        void speak(String sound);
    }
    
    public class DuckHelper{
        public static void teacher(String name, LearnToSpeak trainer){
            trainer.speak(name);
        }
    }
    
    // long version
    public class Duckling{
        public static void makeSound(String sound){
            LearnToSpeak learner = s -> System.out.println(s);
            DuckHelper.teacher(sound, learner);
        }
    }
    
    // short version
    public class Ducking{
        public static void makeSound(String sound){
            LearnToSpeak learner = System.out::println;
            DuckHelper.teacher(sound, learner);
        }
    }
    ```
    
2.  There are four formats for method references. Examples are shown below:
    
    ```java
    // Static Methods
    Consumer<List<Integer>> methodRef = Collections::sort;
    Consumer<List<Integer>> lambda = x -> Collections.sort(x);
    
    // Instance Methods on a Particular Object
    var str = "abc";
    Predicate<String> methodRef = str::startsWith;
    Predicate<String> lambda = s -> str.startsWith(s);
    
    var random = new Random();
    Supplier<Integer> methodRef = random::nextInt;
    Supplier<Integer> lambda = () -> random.nextInt();
    
    // Instance Methods on a Parameter
    Predicate<String> methodRef = String::isEmpty;
    Predicate<String> lambda = s -> s.isEmpty();
    
    // Constructors
    Supplier<List<String>> methodRef = ArrayList::new;
    Supplier<List<String>> lambda = () -> new ArrayList();
    ```
    
3.  Each Java primitive has a corresponding wrapper class. A null value can be assigned to a wrapper class as a null value can be assigned to any reference variable. Attempting to unbox a wrapper class with a null value will cause a NullPointerException.
    
4.  The Diamond Operator is a shorthand notation that allows you to omit the generic type from the right side of a statement when the type can be inferred. An example is shown below:
    
    ```java
    List<Integer> list = new ArrayList<Integer>();
    List<Integer> list = new ArrayList<>();
    ```
    
5.  A collection is a group of objects contained in a single object. The Java Collection Framework is a set of classes in java.util for storing collections. The common
    
    - **List:** Ordered collection of elements that can contain duplicates. Accessed by an int index.
    - **Set:** A collection that does not allow duplicate entries.
    - **Queue:** A collection that orders its elements in a specific order. A typical queue is FIFO.
    - **Map:** A collection that maps keys to values, with no duplicate keys allowed. The elements are key/value pairs.
    - ![hierarchies.png](../_resources/2a6ff92271224391b4da1ac6ae9f520f.png)
6.  The Collection interface and its sub interfaces as well as some implementing classes are shown below. Interfaces are shown in rectangles, with classes in rounded boxes:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table3.1.JPG)![table3.1.JPG](../_resources/6ad9b361d56a4b96a35707a304a68f98.JPG)
    
7.  The Collection interface contains useful convenience methods. These are shown below:
    
    ```java
    boolean add(E element);
    boolean remove(Object object);
    boolean isEmpty();
    int size();
    void clear();
    boolean contains(Object object);
    boolean removeIf(Predicate<? super E> filter);
    void forEach(Consumer<? super T> action);
    ```
    
8.  The *Collections.sort()* method is commonly used when working with collections. To sort objects that you create yourself, Java provides an interface called Comparable. This is shown below:
    
    ```java
    public interface Comparable<T>{
        int compareTo(T o);
    }
    ```
    
9.  The *compareTo()* method returns:
    
    - The number 0 when the current object is equivalent to the argument to *compareTo()*.
    - A negative number when the current object is smaller than the argument to *compareTo()*.
    - A positive number when the current object is larger than the argument to *compareTo()*.
10. An example is shown below:
    
    ```java
    public class MissingDuck implements Comparable<MissingDuck>{
        private String name;
        public int compareTo(MissingDuck quack){
            if(quack == null)
                throw new IllegalArgumentException("Poorly formed duck!");
            if(this.name == null && quack.name == null)
                return 0;
            else if(this.name == null) return -1;
            else if(quack.name == null) return 1;
            else return name.compareTo(quack.name);
        }
    }
    ```
    
11. Note that only one *compareTo()* method can be implemented for a class. If we want to sort by something else, a Comparator can be used. Comparator is a functional interface. An example is shown below:
    
    ```java
    public static void main(String[] args){
        Comparator<Duck> byWeight = new Comparator<Duck>(){
            public int compare(Duck d1, Duck d2){
                return d1.getWeight()-d2.getWeight();
            }
        }
    };
    
    // alternate implementation with lambda
    Comparator<Duck> byWeight = (d1,d2) -> d1.getWeight()-d2.getWeight();
    
    // alternate implementation with method reference
    Comparator<Duck> byWeight = Comparator.comparing(Duck::getWeight);
    
    Collection.sort(ducks, byWeight);
    ```
    
12. A summary of the differences between Comparable and Comparator are shown below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table3.1.JPG)
    
13. When building a comparator there are several helper methods that can be used. These are shown below:
    
    ```java
    reversed();
    thenComparing(function);
    thenComparingDouble(function);
    thenComparingInt(function);
    thenComparing(function);
    ```
    
14. Generics allow you to write and use parametrised types. This allows the compiler to detect issues rather than a ClassCastException exception being thrown.
    
15. Generics can be introduced into classes using angle brackets. An example is shown below:
    
    ```java
    public class Crate<T>{
        private T contents;
        public T emptyCrate(){
            return contents;
        }
        public void packCrate(T contents){
            this.contents = contents;
        }
    }
    ```
    
16. A type parameter can have any name. By convention, the below letters are used:
    
    - E for an element
    - K for a map key
    - V for a map value
    - N for a number
    - T for a generic data type
    - S, U, V etc. for multiple generic types
17. Generics can also be introduced into methods using angle brackets. An example is shown below:
    
    ```java
    public class Handler{
        public static <T> Crate<T> ship(T t){
            System.out.println("Shipping " + t);
            return new Crate<T>();
        }
    }
    ```
    
18. A bounded parameter type is a generic type that specifies a bound for the generic. A wildcard generic type is an unknown generic type represented with a question mark.
    
19. An unbounded wildcard is used when any type is okay. An example is shown below:
    
    ```java
    public static void printList(List<?> list){
        for (Object x:list)
            System.out.println(x);
    }
    ```
    
20. Note that a generic type cannot use a subclass. An example that will not compile is shown below:
    
    ```java
    ArrayList<Number> list = new ArrayList<Integer>();
    ```
    
21. An upper-bounded wildcard can be used to say that any class that extends a class or that class itself can be the parameter type. An example is shown below:
    
    ```java
    public static long total(List<? extends Number> list){
        long count = 0;
        for(Number number:list)
            count += number.longValue();
        return count;
    }
    ```
    
22. Note that due to type erasure the above code is converted to something like:
    
    ```java
    public static long total(List list){
        long count = 0;
        for(Object obj:list)
            Number number = (Number) obj;
            count += number.longValue();
        }
        return count;
    }
    ```
    
23. When upper bounds or unbounded wildcards are used in such a way the list becomes immutable and cannot be modified.
    
24. A lower-bounded wildcard can be used to say that any instance of a class or an instance of a superclass can be the parameter type. An example is shown below:
    
    ```java
    public static void addSound(List<? super String> list){
        list.add("quack");
    }
    
    List<String> strings = new ArrayList<String>();
    strings.add("tweet");
    
    List<Object> objects = new ArrayList<Object>(strings);
    addSound(strings);
    addSound(objects);
    ```
    
25. A useful mnemonic is PECS: Producer Extends, Consumer Super. If you need a List to produce T values (you want to read Ts from the list), you need to declare it using extends. If you need a list to consume T values (you want to write Ts into the list), you need to declare it using super. If you need to both read and write to a list, you need to declare it exactly with no wildcards.
    
26. In the below example, if you want to write elements into the list, you cannot add a Number, Integer or a Double because each one is not compatible with all types. A Number can be read because any of the lists will contain a Number or a subclass of Number. When using extends like this you can only read, and not write.
    
    ```java
    List<? extends Number> foo = new ArrayList<>();
    
    // The foo list could be one of these
    List<? super IOException> foo = new ArrayList<Number>();
    List<? super IOException> foo = new ArrayList<Integer>();
    List<? super IOException> foo = new ArrayList<Double();
    ```
    
27. In the below example, if you want to write elements into the list, you can add an IOException or a FileNotFoundException but not an Exception. This is because an Exception cannot be added to a list of a more specific subclass. An Object can be read from this list but you won't know which type.
    
    ```java
    List<? super IOException> foo = new ArrayList<>();
    
    // The foo list could be one of these
    List<? super IOException> foo = new ArrayList<Exception>();
    List<? super IOException> foo = new ArrayList<IOException>();
    List<? super IOException> foo = new ArrayList<Object>();
    ```
    

### Functional Programming

1.  The functional interfaces shown below are provided as built-in functional interfaces in the java.util.function package:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table4.1.JPG)![table4.1.JPG](../_resources/50dab2b846e34b338b3beafc75cb16da.JPG)
    
2.  A Supplier is used when you want to generate or supply values without taking any input. A supplier is often used to construct new objects. The definition is shown below:
    
    ```java
    @FunctionalInterface
    public interface Supplier<T>{
        T get();
    }
    ```
    
3.  An example for Supplier is shown below:
    
    ```java
    Supplier<LocalDate> s1 = LocalDate::now;
    Supplier<LocalDate> s2 = () -> LocalDate.now();
    
    LocalDate d1 = s1.get();
    LocalDate d2 = s2.get();
    ```
    
4.  A Consumer is used when you want to do something with a parameter but not return anything. A BiConsumer is the same but takes two parameters. The definitions are shown below:
    
    ```java
    @FunctionalInterface
    public interface Consumer<T>{
        void accept(T t);
        // default method omitted
    }
    
    @FunctionalInterface
    public interface BiConsumer<T, U>{
        void accept(T t, U u);
        // default method omitted
    }
    ```
    
5.  An example for Consumer is shown below:
    
    ```java
    Consumer<String> c1 = System.out::println;
    Consumer<String> c2 = x-> System.out.println(x);
    
    c1.accept("Hi");
    c2.accept("Hi");
    ```
    
6.  An example for BiConsumer is shown below:
    
    ```java
    var map = new HashMap<String, Integer>();
    BiConsumer<String, Integer> b1 = map::put;
    BiConsumer<String, Integer> b2 = (k, v) -> map.put(k, v);
    
    b1.accept("chicken", 7);
    b2.accept("chick", 1);
    ```
    
7.  A Predicate is often used when filtering or matching. A BiPredicate is the same but takes two parameters. The definitions are shown below:
    
    ```java
    @FunctionalInterface
    public interface Predicate<T>{
        boolean test(T t);
        // default and static methods omitted
    }
    
    @FunctionalInterface
    public interface BiPredicate<T, U>{
        boolean test(T t, U t);
        // default methods omitted
    }
    ```
    
8.  An example for Predicate is shown below:
    
    ```java
    Predicate<String> p1 = String::isEmpty;
    Predicate<String> p2 = x -> x.isEmpty();
    System.out.println(p1,test(""); // true
    System.out.println(p2,test(""); // true
    ```
    
9.  An example for BiPredicate is shown below:
    
    ```java
    BiPredicate<String, String> b1 = String::startsWith;
    BiPredicate<String, String> b2 = (string, suffix) -> string.startsWith(prefix);
    
    System.out.println(b1.test("chicken", "chick")); // true
    System.out.println(b2.test("chicken", "chick")); // true
    ```
    
10. A Function turns one parameter into a value of a potentially different type and returns it. A BiFunction turns two parameters into a value and returns it. The definitions are shown below:
    
    ```java
    @FunctionalInterface
    public interface Function<T, R>{
        R apply(T t);
        // default and static methods omitted
    }
    
    @FunctionalInterface
    public interface BiFunction<T, U, R>{
        R apply(T t, U u);
        // default method omitted
    }
    ```
    
11. An example for Function is shown below:
    
    ```java
    Function<String, Integer> f1 = String::length;
    Function<String, Integer> f2 = x -> x.length();
    
    System.out.println(f1.apply("cat")); // 3
    System.out.println(f2.apply("cat")); // 3
    ```
    
12. An example for BiFunction is shown below:
    
    ```java
    BiFunction<String, <String, String> b1 = String::concat;
    BiFunction<String, <String, String> b2 = (string, toAdd) -> string.concat(toAdd);
    
    System.out.println(b1.apply("cat ", "dog")); // cat dog
    System.out.println(b2.apply("cat ", "dog")); // cat dog
    ```
    
13. A UnaryOperator is a special case of a Function where all the type parameters are the same type. A BinaryOperator merges two values into one of the same type. The definitions are shown below:
    
    ```java
    @FunctionalInterface
    public interface UnaryOperator<T> extends Function<T, T>{}
    
    @FunctionalInterface
    public interface BinaryOperator<T> extends BiFunction<T,T,T>{
    // omitted static methods
    }
    ```
    
14. An example for UnaryOperator is shown below:
    
    ```java
    UnaryOperator<String> u1 = String::toUpperCase;
    UnaryOperator<String> u2 = x -> x.toUpperCase();
    
    System.out.println(u1.apply("hi")); // HI
    System.out.println(u2.apply("hi")); // HI
    ```
    
15. An example for BinaryOperator is shown below:
    
    ```java
    BinaryOperator<String> b1 = String::concat;
    BinaryOperator<String> b2 = (string, toAdd) -> string.concat(toAdd);
    
    System.out.println(u1.apply("hi ", "there")); // hi there
    System.out.println(u2.apply("hi ", "there")); // hi there
    ```
    
16. The built-in functional interfaces contain various helpful default methods. An example for the Predicate helper methods is shown below with the two statements being equivalent:
    
    ```java
    Predicate<String> combination = s -> s.contains("cat") && ! s.contains("brown");
    Predicate<String> combination = cat.and(brown.negate());
    ```
    
17. An example for the Consumer helper methods is shown below:
    
    ```java
    Consumer<String> c1 = x -> System.out.print("1:" + x);
    Consumer<String> c2 = x -> System.out.print(",2:" + x);
    
    Consumer<String> combined = c1.andThen(c2);
    combined.accept("hi"); // 1:hi,2:hi
    ```
    
18. An example for the Function helper methods is shown below:
    
    ```java
    Function<Integer, Integer> before = x -> x + 1;
    Function<Integer, Integer> after = x -> x * 2;
    
    Function<Integer, Integer> combined = after.compose(before);
    System.out.println(combined.apply(3)); // 8
    ```
    
19. An Optional type is used to express a result that could be "not applicable" without using null references. The Optional instance methods are summarised below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table4.3.JPG)![table4.3.JPG](../_resources/220a432afc444389b40f82825a0dd3b5.JPG)
    
20. An example using the *isPresent()* and *get()* methods is shown below:
    
    ```java
    public static Optional<Double> average(int... scores){
        if(scores.length == 0) return Optional.empty();
        int sum = 0;
        for(int score:scores) sum += score;
        return Optional.of((double) sum/scores.length);
    }
    
    Optional<Double> opt = average(90, 100);
    if(opt.isPresent())
        System.out.println(opt.get()); // 95.0
    ```
    
21. The *ofNullable()* method can be used to return an empty Optional if the value is null:
    
    ```java
    Optional o (value == null) ? Optional.empty() : Optional.of(value);
    Optional o = Optional.ofNullable(value);
    ```
    
22. The *ifPresent()* method can be used to specify a Consumer to be run when there is a value inside of an Optional:
    
    ```java
    Optional<Double> opt = average(90, 100);
    opt.ifPresent(System.out::println);
    ```
    
23. There are multiple methods that can be used to handle an empty Optional. Note that if the value does exist then the value will just be printed. Examples are shown below:
    
    ```java
    Optional<Double> opt = average();
    System.out.println(opt.orElse(Double.NaN)); // NaN
    System.out.println(opt.orElseGet(() -> Math.random())); // random number
    System.out.println(opt.orElseThrow()); // NoSuchElementException
    System.out.println(opt.orElseThrow(
        () -> new IllegalStateException())); // Can throw something else
    ```
    
24. A **stream** in Java is a sequence of data. A stream pipeline consists of the operations that run on a stream to produce a result. A stream can be finite or infinite.
    
25. A stream pipeline consists of:
    
    - **Source:** Where the stream comes from.
    - **Intermediate operations:** Transforms the stream into another one. There can be many intermediate operations. They do not run until the terminal operation runs.
    - **Terminal operations:** Produces a result. A stream can only be used once, the stream is no longer valid after a terminal operation completes.
26. The Stream <t>interface is defined in the java.util.stream package.</t>
    
27. Examples for creating a finite stream are shown below:
    
    ```java
    Stream<String> empty = Stream.empty(); // 0
    Stream<Integer> singleElement = Stream.of(1); // 1
    Stream<Integer> fromArray = Stream.of(1,2,3); // 3
    
    var list = List.of("a","b","c");
    Stream<String> fromList = list.stream();
    Stream<String> fromListParallel = list.parallelStream();
    ```
    
28. Examples for creating an infinite stream are shown below:
    
    ```java
    Stream<Double> randoms = Stream.generate(Math::random);
    Stream<Integer> oddNumbers = Stream.iterate(1, n -> n + 2);
    Stream<Integer> oddNumbersUnder100 = Stream.iterate{
        1, // seed
        n -> n < 100; // Predicate to specify when done
        n -> n + 2; // UnaryOperator to get next value
    }
    ```
    
29. A terminal operation can be performed without an intermediate operation. Reductions are a special type of terminal operation where the contents of the stream are combined into a single primitive or Object. Terminal stream operation method signatures and examples are shown below:
    
    ```java
    // long count()
    Stream<String> s = Stream.of("monkey", "gorilla", "bonobo");
    System.out.println(s.count()); // 3
    
    // Optional<T> min(Comparator<? super T> comparator)
    // Optional<T> max(Comparator<? super T> comparator)
    Stream<String> s = Stream.of("monkey", "ape", "bonobo");
    Optional<String> min = s.min((s1, s2) -> s1.length()-s2.length());
    min.ifPresent(System.out.println); // ape
    
    Optional<?> minEmpty = Stream.empty().min((s1, s2) -> 0);
    System.out.println(minEmpty.isPresent()); // false
    
    // Optional<T> finndAny()
    // Optional<T> findFirst()
    Stream<String> s = Stream.of("monkey", "gorilla", "bonobo");
    Stream<String> infinite = Stream.generate(() -> "chimp");
    s.findAny().ifPresent(System.out:prinln); // monkey (usually)
    infinite.findAny().ifPresent(System.out::println); // chimp
    
    // boolean anyMatch(Predicate<? super T> predicate)
    // boolean allMatch(Predicate<? super T> predicate)
    // boolean noneMatch(Predicate<? super T> predicate)
    
    var list = List.of("monkey", "2", "chimp");
    Stream<String> infinite = Stream.generate(() -> "chimp");
    Predicate<String> pred = x -> Character.isLetter(x.charAt(0));
    
    System.out.println(list.stream().anyMatch(pred)); // true
    System.out.println(list.stream().allMatch(pred)); // false
    System.out.println(list.stream().noneMatch(pred)); // false
    System.out.println(infinite.anyMatch(pred)); // true
    
    // void forEach(Consumer<? super T> action)
    
    Stream<String> s = Stream.of("Monkey", "Gorilla", "Bonobo");
    s.forEach(System.out::print); // MonkeyGorillaBonobo
    
    // T reduce(T identity, BinaryOperator<T> accumulator)
    // Optional<T> reduce(BinaryOperator<T> accumulator)
    // <U> reduce(U identity,
    // BiFunction<U, ? super T, U> accumulator,
    // BinaryOperator<U> combiner)
    
    Stream<String> stream = Stream.of{"w", "o", "l", "f"};
    String word = stream.reduce("", (s,c) -> s + c);
    System.out.println(word); // wolf;
    
    // <R> R collect(Supplier<R> supplier,
    // BiConsumer(<R, ? super T> accumulator,
    // BiConsumer<R, R> combiner)
    // <R, A> R collect(Collector<? super T, A, R> collector)
    
    Stream<String> stream = Stream.of("w", "o", "l", "f");
    TreeSet<String> set = stream.collect(
        Treeset::new,
        Treeset::add,
        Treeset::addAll);
    System.out.println(set); // [f, l, o, w]
    ```
    
30. An intermediate operation produces a stream as its result. Intermediate operation method signatures and examples are shown below:
    
    ```java
    // Stream<T> filter(Predicate<? super T> predicate)
    
    Stream<String> s = Stream.of("monkey", "gorilla", "bonobo");
    s.filter(x -> x.startsWith("m"))
        .forEach(System.out::print); // monkey
    
    // Stream<T> distinct()
    
    Stream<String> s = Stream.of("duck", "duck", "duck", "goose");
    s.distinct()
        .forEach(System.out::print); // duckgoose
    
    // Stream<T> limit(long maxSize)
    // Stream<T> skip(long n)
    
    Stream<Integer> s = Stream.iterate(1, n -> n + 1);
    s.skip(5)
        .limit(2)
        .forEach(System.out::print); // 67
    
    // <R> Stream<R> map(Function<? super T>, ? extends R> mapper)
    Stream<String> s = Stream.of("monkey", "gorilla", "bonobo");
    s.map(String::length)
        .forEach(System.out::print); // 676
    
    // <R> Stream<R> flatMap(
        Function<? super T, ? extends Stream<? extends R>> mapper)
    
    List<String> zero = List.of();
    var one = List.of("Bonobo");
    var two = List.of("Mama Gorilla", "Baby Gorilla");
    Stream<List<String>> animals = Stream.of(zero, one, two);
    
    animals.flatMap(m -> m.stream())
        .forEach(System.out::println);
    
    // Bonobo
    // Mama Gorilla
    // Baby Gorilla
    
    // Stream<T> sorted()
    // Stream<T> sorted(Comparator<? super T> comparator>
    
    Stream<String> s = Stream.of("brown-", "bear-"):
    s.sorted()
        .forEach(System.out:print); // bear-brown-
    
    Stream<String> s = Stream.of("brown bear-", "grizzly-");
    s.sorted(Comparator.reverseOrder())
        .forEach(System.out::print); // grizzly-brown bear-
    
    // Stream<T> peek(Consumer<? super T> action)
    
    var stream = Stream.of("black bear", "brown bear", "grizzly");
    long count = stream.filter(s -> s.startsWith("g"))
        .peek(System.out::println).count() // grizzly
    System.out.println(count); // 1
    ```
    
31. Intermediate and a terminal operation can be chained in a pipeline. An example is shown below:
    
    ```java
    var list = List.of("Toby", "Anna", "Leroy", "Alex");
    list.stream()
        .filter(n -> n.length() == 4)
        .sorted()
        .limit(2)
        .forEach(System.out::println); // AnnaAlex
    ```
    
32. Primitive Streams allow you to work with the int, double and long primitives. They include specialised methods for working with numeric data. The primitive streams are intStream, longStream and doubleStream.
    
33. Primitive streams can be created from other streams. An example is shown below:
    
    ```java
    Stream<String> objStream = Stream.of("penguin", "fish");
    IntStream intStream = objStream.mapToInt(s -> s.length());
    ```
    
34. To create a primitive stream from another stream the below methods are used:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table4.8.JPG)![table4.8.JPG](../_resources/c2f89170b4994667a6272d4c594c672d.JPG)
    
35. The function parameters used when mapping streams are shown below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table4.9.JPG)![table4.9.JPG](../_resources/f0b8167be064423db56b5b67c551db53.JPG)
    
36. Methods can return OptionalDouble, OptionalInt and OptionalLong types when dealing with streams of primitives. A summary of the Optional types for primitives is shown below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table4.10.JPG)![table4.10.JPG](../_resources/1dea7ef1404548d28d35ab5d492de38f.JPG)
    
37. To use multiple terminal operations to produce a result from a stream summary statistic can be used. Summary statistics includes the *getMin()*, *getMax()*, *getAverage()*, *getSum()* and *getCount()* methods. An example is shown below:
    
    ```java
    private static int range(intStream ints){
        IntSummaryStatistics stats = ints.summaryStatistics();
        if(stats.getCount() == 0) throw new RuntimeException();
        return stats.getMax()-stats.getMin();
    }
    ```
    
38. There are special functional interfaces for primitives. The BooleanSupplier functional interface is shown below:
    
    ```java
    // boolean getAsBoolean()
    
    BooleanSupplier b1 = () -> true;
    BooleanSupplier b2 = () -> Math.random() > 0.5;
    System.out.println(b1.getAsBoolean()); // true
    System.out.println(b2.getAsBoolean()); // true or false
    ```
    
39. Common functional interfaces for other primitives are shown below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table4.11.JPG)![table4.11.JPG](../_resources/1bd98457fd50487eb38c1017b6deb735.JPG)
    
40. Common functional interfaces for other primitives are shown below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table4.12.jpg)![table4.12.jpg](../_resources/e93027064f2f4f9dbbee4e52a93ae2e1.jpg)
    
41. Predefined collectors are available via static methods on the Collectors interface. These are shown below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table4.13.jpg)![table4.13.jpg](../_resources/2bf34fdb09cf4c7bb4237d90d87f9dc8.jpg)
    
42. Examples for using collectors are shown below:
    
    ```java
    var ohMy = Stream.of("lions", "tigers", "bears");
    String result = ohMy.collect(Collectors.joining(", "));
    System.out.println(result); // lions, tigers, bears
    
    var ohMy = Stream.of("lions", "tigers", "bears");
    String result = ohMy.collect(Collectors.averagingInt(String::length));
    System.out.println(result); // 5.333333333333
    
    var ohMy = Stream.of("lions", "tigers", "bears");
    TreeSet<String> result = ohMy
        .filter(s -> s.startsWith("t))
        .collect(Collectors.toCollection(TreeSet::new));
    System.out.println(result); // [tigers]
    
    var ohMy = Stream.of("lions", "tigers", "bears");
    Map<String, Integer> map = ohMy.collect(
        Collectors.toMap(s -> s, String::length));
    Systemout.println(map); // {lions=5, bears=5, tigers=6}
    
    var ohMy = Stream.of("lions", "tigers", "bears");
    Map<Integer, String> map = ohMy.collect(Collectors.toMap(
        String::length,
        k -> k,
        (s1, s2) -> s1 + "," + s2));
    System.out.println(map); // {5=lions,bears, 6=tigers}
    System.out.println(map.getClass()); // class java.util.HashMap
    
    var ohMy = Stream.of("lions", "tigers", "bears");
    Map<Integer, List<String>> map = ohMy.collect(
        Collectors.groupingBy(String::length));
    System.out.println(map); // {5=[lions, bears], 6=[tigers]}
    
    var ohMy = Stream.of("lions", "tigers", "bears");
    Map<Boolean, List<String> map = ohMy.collect(
        Collectors.partitioningBy(s -> s.length() <= 5));
    System.out.println(map); // {false=[tigers], true=[lions, bears]}
    ```
    

### Exceptions, Assertions, and Localization

1.  A custom exception class can be created by extending Exception (for a checked exception), or RuntimeException (for an unchecked exception).
    
2.  A try-with-resources statement ensures that any resources declared in the try block are automatically closed at the conclusion of the try block. A resource is typically a file or a database that requires a stream or connection to read or write data.
    
3.  To be used in a try-with-resources statement the resource is required to implement the `AutoClosable` interface. Inheriting `AutoClosable` requires implementing a `close()` method. If multiple resources are included in a try-with-resources statement they are closed in the reverse order in which they are declared.
    
4.  It is possible to use resources declared prior to a try-with-resources statement, provided they are marked final or are effectively final. The syntax is to use the resource name in place of the resource declaration, separated by a semicolon.
    
5.  An assertion is a Boolean expression that you place where you expect something to be true. An assert statement contains this statement along with an optional message. An assertion allows for detecting defects in the code. You can turn on assertions for testing and debugging while leaving them off when your program is in production. Unit tests are most frequently used to verify behaviour, whereas assertions are commonly used to verify the internal state of a program.
    
6.  Assertions should never alter outcomes. Assertions should be turned off in a production environment.
    
7.  The syntax for an assertion is shown below:
    
    ```java
    assert test_value;
    assert test_value: message;
    ```
    
8.  An assertion evaluating to false will result in an AssertionError being thrown at runtime if assertions are enabled. To enable assertions a flag can be passed as per the below:
    
    ```java
    java -enableassertions Rectangle
    java -ea Rectangle
    ```
    
9.  Assertions can be enabled or disabled for specific classes or packages.
    
    ```java
    java -ea:com.demos... my.programs.Main // enable for classes in the com.demos package and any subpackages
    java -ea:com.demos... -da:com.demos.TestColors my.programs.Main // enable for com.demos but disables in TestColors class
    ```
    
10. Java includes numerous classes for dates and times:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table5.4.JPG)![table5.4.JPG](../_resources/243ad700ab9b43419a92f7790109a657.JPG)
    
11. Each of these types contains a *now()* method to get the current date or time and an *of()* method to instantiate an object. Various get methods are also provided.
    
12. The *format()* method can take a DateTimeFormatter to display standard or custom formats. Note that enclosing values in single quotes escapes the values. Examples are shown below:
    
    ```java
    LocalTime time = LocalTime.of(11, 12, 34);
    LocalDate date = LocalDate.of(2020, Month.OCTOBER, 20);
    System.out.println(time.format(DateTimeFormatter.ISO_LOCAL_TIME)); // standard format example
    var f = DateTimeFormatter.ofPattern("MMMM dd, yyyy 'at' hh:mm");
    System.out.println(dt.format(f)); // October 20, 2020 at 11:12
    ```
    
13. Supported symbols for each date and time class are shown below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table5.6.JPG)![table5.6.JPG](../_resources/73ed390ea5794b45a7b213fb130a03c0.JPG)
    
14. Internationalisation is the process of designing a program so that it can be adapted. Localisation means supporting multiple locales or geographic regions. Examples for working with locales are shown below:
    
    ```java
    Locale locale = Locate.getDefault();
    System.out.println(locale); // en_US
    System.out.println(Locate.GERMAN); // de
    System.out.println(Locale.GERMANY); // de_DE
    ```
    
15. Formatting or parsing currency and number values can change depending on the locale. Methods to get a number format based on a locale are shown below:
    
    ![table5.7.JPG](../_resources/5d1a722079bd48bfaf05c8e2a7f1b3ab.JPG)![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table5.7.JPG)
    
16. An example of their usage is shown below:
    
    ```java
    int attendeesPerYear = 3_200_000;
    int attendeesPerMonth = attendeesPerYear / 12; 
    var us = NumberFormat.getInstance(Locale.US);
    System.out.println(us.format(attendeesPerMonth)); // 266,666
    var gr = NumberFormat.getInstance(Locale.GERMANY);
    System.out.println(gr.format(attendeesPerMonth)); /// 266.666
    ```
    
17. The DecimalFormat class can be used to express currency. A *#* is used to omit the position if no digit exists, and a 0 is used to place a 0 in the position if no digit exists. Examples are shown below:
    
    ```java
    double d = 1234567.467;
    NumberFormat f1 = new DecimalFormat("###,###,###.0");
    System.out.println(f1.format(d)); // 1,234,567.5
    ```
    
18. Date formats can also vary by locale. Methods used to retrieve an instance of DateTimeFormatter using the default locale are shown below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table5.9.JPG)![table5.9.JPG](../_resources/ae5fddd93e114faab68ca20234f48de2.JPG)
    
19. A resource bundle contains locale-specific objects used by a program. It is commonly stored in a properties file. A properties file is a text file in a specific format with key/value pairs.
    
20. An example using two property files is shown below:
    
    ```java
    Zoo_en.properties // name of file
    hello=Hello
    open=The zoo is open
    
    Zoo_fr.properties // name of file
    hello=Bonjour
    open=Le zoo est ouvert
    
    public static void printWelcomeMessage(Locale locale){
        var rb = ResourceBundle.getBundle("Zoo", locale);
        System.out.println(rb.getString("hello") + "," + rb.getString("open"));
    }
    
    public static void main(String[] args){
        var us = new Locale("en", "US");
        var france = new Locale("fr", "FR");
        printWelcomeMessage(us);
        printWelcomeMessage(france);
    }
    ```
    
21. To find a resource bundle to use Java looks for the language/country in the filename, followed by just the language. The default resource bundle is used if no matching locale can be found.
    

### Modular Applications

1.  There are three types of modules:
    
    - **Named Modules:** Contains a module-info file which appears in the root of the JAR alongside one or more packages. Unless otherwise specified, a module is a named module. Named modules appear on the module path rather than the classpath.
    - **Automatic Module:** Appears on the module path but does not contain a module-info file. It is a regular JAR file that is placed on the module path and gets treated as a module. The code referencing an automatic module treats it as if there is a module-info present, and automatically exports all packages. If an Automatic-Module-Name is specified in the manifest, then that name is used. Otherwise, a module name is automatically determined based on the JAR filename. To determine the name the file extension is removed, then the version number, and then special characters are replaced with a period. If a period is the first or last character it is also removed.
    - **Unnamed Module:** Like an automatic module, it is a regular JAR file. An unnamed module is on the classpath rather than the module path. An unnamed module does not usually contain a module-info file, and if it does, it is ignored since it is on the classpath. Unnamed modules do not export any packages to named or automatic modules, and an unnamed module can read from any JARs on the classpath or module path.
2.  Modules prefixed with *java* (standard modules) are shown below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table6.5.JPG)![table6.5.JPG](../_resources/e477ab58766b45aeac9cb18c0d0a654e.JPG)
    
3.  Modules prefixed with *jdk* (part of the JDK) are shown below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table6.6.JPG)![table6.6.JPG](../_resources/9bcc9116018f48b08e7fcc29c6c6dec1.JPG)
    
4.  The *jdeps* command provides information about dependencies. An example is shown below:
    
    ```java
    // Animatronic.java
    
    import java.time.*;
    import java.util.*;
    import sun.misc.Unsafe;
    
    public class Animatronic {
        private List<String> names;
        private LocalDate visitDate;
    
        public Animatronic(List<String> names, LocalDate visitDate){
            this.names = names;
            this.visitDate = visitDate;
        }
    
        public void unsafeMethod(){
            Unsafe unsafe = Unsafe.getUnsafe();
        }
    }
    ```
    
    ```shell
    javac *.java
    jar -cvf zoo.dino.jar .
    jdeps zoo.dino.jar
    ```
    
5.  Before older applications can be migrated to use modules, the structure of the packages and libraries in the existing application need to be determined. In the below diagram style the arrows point from the project that will require the dependency to the one that makes it available. Projects that do not have any dependencies are at the bottom.
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/figure6.4.JPG)
    
6.  A bottom-up migration is the easiest migration approach. It works when you have the power to convert any JAR files that are not already modules. The approach is:
    
    - Pick the lowest-level project that has not yet been migrated.
    - Add a module-info.java file to that project. Be sure to add any exports to expose any package used by higher level JAR files. Also, add the requires directive for any modules it depends on.
    - Move this newly migrated named module from the classpath to the module path.
    - Ensure any projects that have not yet been migrated stay as unnamed modules on the classpath.
    - Repeat with the next-lowest-level project until you are done.
7.  A top-down migration is most useful when you do not have control of every JAR file used by your application. The approach is:
    
    - Place all projects on the module path.
    - Pick the highest-level project that has not yet been migrated.
    - Add a module-info file to that project to convert the automatic module into a named module. Remember to add any exports or requires directives. Automatic module names can be used when writing the requires directive since most of the projects on the module path do not have names yet.
    - Repeat with the next-highest-level project until you are done.
8.  An example of the bottom-up migration approach (left) and top-down migration approach (right) is shown below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/figure6.7.JPG)![table6.8.JPG](../_resources/f119701c2cb54c2fbfb80a130ef071e4.JPG)
    
9.  When splitting up a project into modules, a problem with **cyclic dependencies** may arise. A cyclic dependency occurs when 2 or more things have dependencies on each other. Modules that have cyclic dependencies will not compile. A common technique to resolve this issue is to introduce another module containing all the code that the modules share. Note that a cyclic dependency can still exists between packages with a module.
    
10. Although not recommended, is possible to customise what packages a module exports from the command line.
    
    ```java
    javac --add-reads moduleA=moduleB --add-exports moduleB/com.modB.package1=moduleA ...
    java --add-reads moduleA=moduleB --add-exports moduleB/com.modB.package1=moduleA ...
    // --add-reads moduleA=moduleB implies that moduleA wants to read all exported packages of moduleB
    // add-exports moduleB/com.modB.package1=moduleA implies that moduleB exports package com.modB.package1 to moduleA
    // add-open is used ot provide access to privat members of classes through reflection (not required for exam)
    ```
    
11. The previous section discussed modules in terms of dependencies, with one module exporting its public types and another module requiring them. This is a very tight coupling. A looser coupling can be if one module requires an implementation of an interface from another module, and the other module provides that implementation.
    
12. A **service** is composed of an interface, classes referenced by the interface references, and a way to look up the implementations of the interface. A sample tours application will be used to introduce this concept. The 4 modules within this application are shown below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/figure6.10.JPG)
    
13. A **service provider interface** specifies the behaviour that the service will have. The service provider interface is exported for other modules to use. For the tours application this is shown below:
    
    ```java
    // Souvenir.java
    package zoo.tours.api;
    
    public class Souvenir{
        private String description;
    
        public String getDescription(){
            return description;
        }
    
        public void setDescription(String description){
            this.description = description;
        }
    }
    
    // Tour.java
    package zoo.tours.api;
    
    public interface Tour {
        String name();
        int length();
        Souvenir getSouvenir();	
    }
    
    // module-info.java
    module zoo.tours.api{
        exports zoo.tours.api;
    }
    ```
    
14. A **service locator** can find any classes that implement a service provider interface. At runtime, there may be many service providers (or none) that are found by the service locator. The service locator requires the service provider interface package, uses the Tour class to lookup classes that implement a service provider interface, and exports the package with the lookup for other modules to use. For the tours application this is shown below:
    
    ```java
    // TourFinder.java
    package zoo.tours.reservations;
    
    import java.util.*;
    import zoo.tours.api.*;
    
    public class TourFinder{
        
        public static Tour findSingleTour(){
            ServiceLoader<Tour> loader = ServiceLoader.load(Tour.class);
            for(Tour tour : loader)
                return tour;
            return null;
        }
    
        public static List<Tour> findAllTours(){
            List<Tour> tours = new ArrayList<>();
            ServiceLoader<Tour> loader = ServiceLoader.load(Tour.class);
            for(Tour tour : loader)
                tours.add(tour);
            return tours;
        }
    }
    
    // module-info.java
    module zoo.tours.reservations {
        exports zoo.tours.reservations;
        requires zoo.tours.api;
        uses zoo.tours.api.Tour;
    }
    ```
    
15. A **consumer** refers to a module that obtains and uses a service. Once the consumer has acquired a service via the service locator, it is able to invoke the methods provided by the service provider interface. The consumer requires service provider interface and the service locator. For the tours application this is shown below:
    
    ```java
    // Tourist.java
    package zoo.visitor;
    
    import java.util.*;
    import zoo.tours.api.*;
    import zoo.tours.reservations.*;
    
    public class Tourist{
        public static void main(String[] args){
            Tour tour = TourFinder.findSingleTour();
            System.out.println("Single tour: " + tour);
        
            List<Tour> tours = TourFinder.findAllTours();
            System.out.println("# tours: " + tours.size());
        }
    }
    
    // module-info.java
    module zoo.visitor{
        requires zoo.tours.api;
        requires zoo.tours.reservations;
    }
    ```
    
16. A **service provider** is the implementation of a service provider interface. The service provider requires the service provider interface, and provides an implementation of the behaviour specified in the service provider interface. Note that the export directive is not used as we do not want consumers referring to the service provider directly. For the tours application this is shown below:
    
    ```java
    // TourImpl.java
    package zoo.tours.agency;
    
    import zoo.tours.api.*;
    
    public class TourImpl implements Tour{
        public String name(){
            return "Behind the Scenes";
        }
    
        public int length(){
            return 120;
        }
    
        public Souvenir getSouvenir(){
            Souvenir gift = new Souvenir();
            gift.setDescription("stuffed animal");
            return gift;
        }
    }
    
    // module-info.java
    module zoo.visitor{
        requires zoo.tours.api;
        provides zoo.tours.api.Tour with zoo.tours.agency.TourImpl;
    }
    ```
    
17. If a service provider declares a provider method, then the service loader invokes that method to obtain an instance of the service provider. A provider method is a public static method named "provider" with no formal parameters and a return type that is assignable to the service's interface or class. In this case, the service provider **need not** be assignable to the service's interface or class.
    
18. If a service provider does not declare a provider method, then the service provider is instantiated directly, via its constructor. There must be a service provider constructor that takes no arguments and is assignable to the service's interface or class. The provides directive in a service provider cannot specify the same service more than once.
    
19. If the used directive occurs in a class, the *ServiceLoader.load()* method returns a ServiceLoader object that can provide instances of the service type. The module system automatically discovers provider modules at start up by scanning modules in the Java runtime image and modular jars in the module path. As there can be multiple implementations of the service, multiple instances of the service type can be returned. The service type should offer enough descriptor methods for a consumer to select the best implementation.
    
20. The requires directive takes an object name, the exports directive takes a package name, the uses directive takes a type name, and the provides directive takes a service type and provider class. A consumer module will contain requires/uses, while a provider module will contain requires/provides.
    
21. A summary of the directives required for reach service artefact is shown below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/table6.8.JPG)
    

### Concurrency

1.  Disk and network operations are extremely slow compared to CPU operations. Multithreaded processing is used by modern operating systems to allow applications to execute multiple tasks at the same time, which allows tasks waiting for resources to give way to other processing requests. Java has traditionally supported multithreaded programming using the **Thread** class. The **Concurrency** API has grown over time to provide numerous classes for performing complex thread-based tasks.
    
2.  A thread is the smallest unit of execution that can be scheduled by the operating system. A process is a group of associated threads that execute in the same, shared environment. A **task** is a single unit of work performed by a thread.
    
3.  A process model is shown below:
    
    ![](/C:/Users/dmartodikromo/AppData/Local/Programs/Joplin/resources/app.asar/res/figure7.1.JPG)
    
4.  Thread types include **system threads** threads created by the JVM, and **user-defined** threads which are created by the application developer. Operating systems use a **thread scheduler** to determine which threads should be executing. A **context switch** is the process of storing a thread's current state and later restoring the state of the thread to continue executing. A thread can interrupt or supersede another thread if it has a higher **thread priority**.
    
5.  The *java.lang.Runnable* interface is a functional interface that takes no arguments and returns no data. It is commonly used to define the task or work that a thread will execute, separate from the main application thread. The definition of runnable is shown below:
    
    ```java
    @FunctionalInterface 
    public interface Runnable {
        void run();
    }
    ```
    
6.  To execute a thread first you define an instance of *java.lang.Thread*, and then you start the task using the *Thread.start()* method. Examples of defining a thread are shown below:
    
    ```java
    // Providing a Runnable object to the Thread constructor
    public class PrintData implements Runnable{
        @Override public void run() {
            for(int i = 0; i < 3; i++)
                System.out.println("Printing record: "+i);
        }
    
        public static void main(String[] args){
            (new Thread(new PrintData())).start();
    }
    
    // Creating a class that extends Thread and overrides the run() method
    public class ReadInventoryThread extends Thread{
        @Override public void run() {
            System.out.println("Printing zoo inventory");
        }
    
        public static void main(String[] args){
            (new ReadInventoryThread()).start();
        }
    }
    ```
    
7.  While threads operate asynchronously, one thread may need to wait for the results of another thread. In such a case the *Thread.sleep()* method can be used to make a thread pause until results are ready. An example is shown below:
    
    ```java
    class CheckResults {
        private static int counter = 0;
    
        public static void main(String[] a) throws InterruptedException {
        new Thread(() -> {
            for (int i = 0; i < 500; i++) {
            CheckResults.counter++;
            }
        }).start();
        while (CheckResults.counter < 100) {
            System.out.println("Not reached yet");
            Thread.sleep(1000); // 1 SECOND
        }
        System.out.println("Reached!");
        }
    }
    ```
    
8.  To improve on the above and to assist with creating and managing threads, the *ExecutorService* interface in the Concurrency API can be used.
    
9.  An example of using *newSingleThreadExecutor()* is shown below:
    
    ```java
    import java.util.concurrent.*;
    public class ZooInfo{
        public static void main(String[] args){
            ExecutorService service = null;
            Runnable task1 = () ->
                System.out.println("Printing zoo inventory");
            Runnable task2 = () -> {for(int i = 0; i < 3; i++)
                System.out.println("Printing record: "+i);};
    
            try{
                service = Executors.newSingleThreadExecutor();
                System.out.println("begin");
                service.execute(task1);
                service.execute(task2);
                service.execute(task1);
                System.out.println("end");
            } finally {
                if(service != null) service.shutdown();
            }
        }
    }
    ```
    
10. If the *shutdown()* method is not called then the application will never terminate. As part of shutdown the thread executor rejects any new tasks submitted to the thread executor while continuing to execute any previously submitted tasks. The *isShutdown()* and *isTerminated()* methods can be used to check the status of the thread. The *shutdownNow()* method attempts to stop all running tasks immediately.
    
11. Tasks can be submitted to an *ExecutorService* in multiple ways. The *execute()* method is inherited from the *Executor* interface, which the *ExecutorService* interface extends. It is considered a "fire-and-forget" method as once it is submitted the result is not directly available to the calling thread. The *submit()* method returns a *Future* instance that can be used to determine whether the task is complete.
    
12. Useful *ExecutorService* methods are shown below:
    
    ```java
    void execute(Runnable command);
    Future<?> submit(Runnable task);
    <T> Future<T> submit(Callable<T> task);
    <T> List<Future<T>> invokeAll(Collections<? extends Callable<T>> tasks) throws InterruptedException;
    <T> T invokeAny(Collection<? extends Callable<T>> tasks) throws InterruptedException, ExecutionException;
    ```
    
13. To improve on the previous CheckResults implementation and avoid managing threads directly, the below implementation using *submit()* to return a *Future* object can be used:
    
    ```java
    public class CheckResults {
        private static int counter = 0;
    
        public static void main(String[] unused) throws Exception {
        ExecutorService service = null;
        try {
            service = Executors.newSingleThreadExecutor();
            Future<?> result = service.submit(() -> {
            for (int i = 0; i < 500; i++) {
                CheckResults.counter++;
            }
            });
            result.get(10, TimeUnit.SECONDS);
            System.out.println("Reached!");
        } catch (TimeoutException e) {
            System.out.println("Not reached in time");
        } finally {
            if (service != null) {
            service.shutdown();
            }
        }
        }
    }
    ```
    
14. The *java.util.concurrent.Callable* functional interface is similar to *Runnable* except that its *call()* method returns a value and can throw a checked exception. The definition of the *Callable* interface is shown below:
    
    ```java
    @FunctionalInterface
    public interface Callable<V> {
        V call() throws Exception;
    }
    ```
    
15. The *Callable* interface is often preferable over *Runnable* since it allows more details to be retrieved easily from the task after it is completed.
    
16. After submitting tasks to a thread executor, it is common to wait for the results. An example is shown below for a simple generic pattern where the result from the thread executor doesn't need to be retained:
    
    ```java
    ExecutorService service = null;
    try {
        service = Executors.newSingleThreadExecutor();
        // Add tasks to the thread executor
    } finally {
        if (service != null) {
        service.shutdown();
        }
    }
    if (service != null) {
        service.awaitTermination(1, TimeUnit.MINUTES);
        // Check whether all tasks are finished
        if (service.isTerminated()) {
        System.out.println("Finished!");
        } else {
        System.out.println("At least one task is still running");
        }
    }
    ```
    
17. The *invokeAll()* and *invokeAny()* methods can be used to execute task collections synchronously. The *invokeAll()* method will wait indefinitely until all tasks are complete, while the *invokeAny()* method will wait indefinitely until at least one task completes.
    
18. The *ScheduledExecutorService* can be used to schedule a task to happen at some future time. Useful *ScheduledExecutorService* methods are shown below:
    
    ```java
    schedule(Callable<V> callable, long delay, TimeUnit unit);
    schedule(Runnable command, long delay, TimeUnit unit);
    scheduleAtFixedRate(Runnable command, long initialDelay, long period, TimeUnit unit);
    scheduleWithFixedDelay(Runnable command, long initialDelay, long delay, TimeUnit unit);
    ```
    
19. An example usage of *ScheduledExecutorService* is shown below:
    
    ```java
    ScheduledExecutorService service = Executors.newSingleThreadScheduledExecutor();
    Runnable task1 = () -> System.out.println("Hello zoo");
    Callable<String> task2 = () -> "Monkey";
    ScheduledFuture<?> r1 = service.schedule(task1, 10, TimeUnit.SECONDS);
    ScheduledFuture<?> r2 = service.schedule(task2, 8, TimeUnit.MINUTES);
    ```
    
20. Additional factory methods in the *Executors* class are available that use a pool of threads. A *thread pool* is a group of pre-instantiated reusable threads that are available to perform a set of tasks. Useful *ScheduledExecutorService* factory methods are shown below:
    
    ```java
    ExecutorService.newSingleThreadExecutor();
    ScheduledExecutorService.newSingleThreadScheduledExecutor();
    ExecutorService.newCachedThreadPool();
    ExecutorService.newFixedThreadPool(int);
    ScheduledExecutorService.newScheduledThreadPool(int);
    ```
    
21. An instance of a pooled-thread executor will execute concurrently if the number of tasks is less than the number of available threads. Calling *newFixedThreadPool()* with a value of 1 is equivalent to calling *newSingleThreadExecutor()*. The number of threads in the pool is often set to equal the number of available CPUs.
    
22. Thread-safety is the property of an object that guarantees safe execution by multiple threads at the same time. As threads run in a shared environment and memory space, data must be organised so that we do not end up with unexpected results.
    
23. An example of non-thread safe code is shown below:
    
    ```java
    public class SheepManager {
        private int sheepCount = 0;
    
        private void incrementAndReport() {
            System.out.print((++sheepCount) + " ");
        }
    
        public static void main(String[] args) {
            ExecutorService service = null;
            try {
                service = Executors.newFixedThreadPool(20);
                SheepManager manager = new SheepManager();
                for (int i = 0; i < 10; i++) {
                    service.submit(() -> manager.incrementAndReport());
                }
            } finally {
                if (service != null) {
                    service.shutdown();
                }
            }
        }
    }
    ```
    
24. Multiple threads read and write the sheepCount variable, with one of the threads overwriting the results of the others. When 2 or more threads execute the right side of the expression, only the result of one of the increment operations is stored. This is known as a **race condition** and means the output will be different each time.
    
25. *Atomic* is the property of an operation to be carried out as a single unit of execution without any interference by another thread. The *java.util.concurrent.atomic* package contains the following useful Atomic classes:
    
    ```java
    AtomicBoolean
    AtomicInteger
    AtomicLong
    ```
    
26. Each class contains numerous methods that equivalent to many of the primitive built-in operators. Common atomic methods (e.g. for AtomicInteger) are shown below:
    
    ```java
    int get();
    void set(int);
    int getAndSet(int);
    int incrementAndGet();
    int getAndIncrement();
    int decrementAndGet();
    int getAndDecrement()
    ```
    
27. Replacing *++sheepCount* and the int declaration with *sheepCount.incrementAndGet()* and an AtomicInteger declaration results in all of the numbers being printed, but the order is still not guaranteed. No increment operation is lost but we do not know which thread will return first.
    
28. A monitor (or lock) is a structure that supports *mutual exclusion*, which is the property that at most one thread is executing a particular segment of code at a given time. As each thread arrives at a lock it checks if any threads are already in the block, and only a single thread can hold the lock. Adding the synchronized block as per the below will ensure the output of the above is sequential:
    
    ```java
    private void incrementAndReport() {
        synchronized(this) {
            System.out.print((++sheepCount) + " ");
        }
    }
    ```
    
29. The synchronized modifier can also be added to a method to achieve the same effect. A static synchronized block can also be used if thread access needs to be ordered across all instances, and not just a single instance.
    
30. Correctly using the synchronised keyword can be challenging and has performance implication. Other classes within the Concurrency API that are easier to use are recommended.
    
31. The Concurrency API includes the *lock* interface that is conceptually like using the synchronized keyword, but that has a lot more features. The below blocks are equivalent:
    
    ```java
    // Implementation #1 with a synchronized block
    Object object = new Object();
    synchronized (object) {
        // protected code
    }
    
    // Implementation #2 with a Lock
    Lock lock = new ReentrantLock();
    try {
        lock.lock();
        // protected code
    } finally {
        lock.unlock();
    }
    ```
    
32. Useful lock interface methods include:
    
    ```java
    void lock();
    void unlock();
    boolean tryLock();
    boolean tryLock(long, TimeUnit);
    ```
    
33. The *tryLock()* method attemps to acquire a lock and immediately returns a *boolean* result. It does not wait if another thread already holds the lock, it returns immediately whether a lock is available. The *tryLock(long, TimeUnit)* method is similar but will wait for a period of time to acquire the lock. An example for *tryLock()* is shown below:
    
    ```java
    Lock lock = new ReentrantLock();
    new Thread(() -> printMessage(lock)).start();
    if (lock.tryLock()) {
        try {
            System.out.println("Lock obtained, entering protected code");
        } finally {
            lock.unlock();
        }
    } else {
        System.out.println("Unable to acquire lock, doing something else");
    }
    ```
    
34. The *CyclicBarrier* class can be used to allow a set of threads to wait for each other to reach a common execution point, known as a barrier. This allows multiple threads to still run. An example is shown below:
    
    ```java
       public class LionPenManager {
        private void removeLions() {
            System.out.println("Removing lions");
        }
    
        private void cleanPen() {
            System.out.println("Cleaning the pen");
        }
    
        private void addLions() {
            System.out.println("Adding lions");
        }
    
        public void performTask(CyclicBarrier c1, CyclicBarrier c2) {
            try {
                removeLions();
                c1.await();
                cleanPen();
                c2.await();
                addLions();
            } catch (InterruptedException | BrokenBarrierException e) {
                // handle
            }
        }
    
        public static void main(String[] args) {
            ExecutorService service = null;
            try {
                service = Executors.newFixedThreadPool(4);
                var manager = new LionPenManager();
                var c1 = new CyclicBarrier(4);
                var c2 = new CyclicBarrier(4, () -> System.out.println("*** Pen Cleaned!"));
                for (int i = 0; i < 4; i++) {
                    service.submit(() -> manager.performTask(c1, c2));
                }
            } finally {
                if (service != null) {
                    service.shutdown();
                }
            }
        }
    }
    ```
    
35. The Concurrency API also includes interfaces and classes to help solve common memory consistency errors. A *memory consistency* error occurs when two threads have inconsistent views of what should be the same data. The JVM may throw a *ConcurrentModificationException* in such a scenario. An example is shown below:
    
    ```java
    // ConcurrentModificationException thrown
    var foodData = new HashMap<String, Integer>();
    foodData.put("penguin", 1);
    foodData.put("flamingo", 2);
    for(String key: foodData.keySet()) {
        foodData.remove(key);
    }
    
    // No exception thrown
    var foodData = new ConcurrentHashMap<String, Integer>();
    foodData.put("penguin", 1);
    foodData.put("flamingo", 2);
    for(String key: foodData.keySet()) {
        foodData.remove(key);
    }
    ```
    
36. In the above example the iterator on *keySet()* is not properly updated after the first element is removed, so an exception is thrown. Concurrent collection classes should be used any time multiple threads are going to modify a collections object outside of a *synchronized* block. Concurrent collection classes are shown below:
    
    ```java
    ConcurrentHashMap
    ConcurrentLinkedQueue
    ConcurrentSkipListMap
    ConcurrentSkipListSet
    CopyOnWriteArrayList
    CopyOnWriteArraySet
    LinkedBlockingQueue
    ```