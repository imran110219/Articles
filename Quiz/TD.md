## Java

#### Q1. Variables declared as ....... cannot exist on a per-instance basis.

- [ ] Static
- [x] Final
- [ ] Abstract
- [ ] Code

**Reasoning:** The substring method is accepting two arguments.

#### Q2. Which lines will cause errors when this code is compiled?

```
abstract class Animal {
    public abstract void makeNoise();
    public abstract void move();
}

abstract class Canine extends Animal {
    public void wagTail() {
        System.out.println("Wagging");
    }

    @Override
    public void move() {
        System.out.println("Run");
    }
}

class Dog extends Canine {

    public void fetch() {
        System.out.println("Fetch");
    }

    @Override
    public void makeNoise() {
        System.out.println("Bark");
    }
}

public class Question2 {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.makeNoise();
        d.move();
        d.wagTail();
        d.fetch();

        Canine c = new Dog();
        c.makeNoise();
        c.move();
        c.wagTail();
        c.fetch();

        Animal a = new Dog();
        a.makeNoise();
        a.move();
        a.wagTail();
        a.fetch();
    }
}
```

What is the result if we attempt compile this code?

- [x] `c.fetch();`
- [ ] `a.move();`
- [ ] `Canine c = new Dog(); Animal a = new Dog();` // You Cannot Assign an Object of Type Dog to a Variable Declared as typeAnimal
- [x] `a.wagTail(); a.fetch();`

**Reasoning:** The substring method is accepting two arguments.

#### Q3. Which of the following are unchecked exceptions in Java.

(Select all that apply.)

- [ ] Runtime Exception
- [x] ClassCast Exception
- [ ] NullPointer Exception
- [ ] IOException

**Reasoning:** The substring method is accepting two arguments.

#### Q4. Consider the following program:

```
package com.turing.java;

public class Test {
    public static void main(String[] args) {
        Super s = new Subclass();
        s.foo();
    }
}

class Super {

    public void foo() {
        System.out.println("Super");
    }
}

class Subclass extends Super {
    static void foo() {
        System.out.println("Subclass");
    }
}
```

What is the output?

- [ ] Super
- [ ] Subclass
- [ ] Runtime Error
- [x] Compile Time Error

**Reasoning:** The substring method is accepting two arguments.

#### Q5. Which of the following doesn't have an index-based structure?

- [ ] List
- [x] Map
- [ ] Set
- [ ] TreeMap

**Reasoning:** The substring method is accepting two arguments.

#### Q6. Consider the following program:

```
abstract class demo {
    public int a;
    demo(){
        a = 10;
    }
    abstract final public void get();
}

class Test extends demo {
    final public void get() {
        System.out.println("a = " + a);
    }

    public static void main(String[] args) {
        Test obj = new Test();
        obj.get();
    }
}

```

What is the output?

- [ ] 30
- [ ] 10
- [ ] 20
- [x] Compilation Error

**Reasoning:** The substring method is accepting two arguments.

#### Q7. What is the output of the following code?

```
List<String> list1 = new ArrayList();
list1.add("foo");

List<String> list2 = list1;
List<String> list3 = new ArrayList(list2);

list1.clear();
list2.add("bar");
list3.add("baz");

System.out.print(list1);
System.out.print(list2);
System.out.print(list3);
```

- [ ] [bar], [bar], [foo, baz]
- [ ] [bar, baz], [bar, baz], [bar, baz]
- [ ] [], [bar], [foo, baz]
- [x] [], [bar], [bar, baz]

**Reasoning:** The substring method is accepting two arguments.

#### Q8. Which of the following declarations of an array contains an error?

- [ ] int x[] = int[10];
- [ ] int[] y = new int[5];
- [ ] float d[] = {1, 2, 3};
- [x] int a[] = {1, 2, 3}; int b[]; b=a;

**Reasoning:** The substring method is accepting two arguments.

#### Q10. The ........... statement can be used to handle an exception that is not caught by any of the prevoius catch statements.

- [ ] Catch
- [ ] Throw
- [ ] Finally
- [x] Try

**Reasoning:** The substring method is accepting two arguments.

#### Q20. What will happen if we call the `run()` method instead of calling the `start()` method when starting a thread?

- [ ] Each thread starts in a seperate call stack.
- [x] If we invoke the run() method from the main thread, run() method will go on to the current call stack rather than going to the begining of a new call stack.
- [ ] Both A & B
- [ ] None of the above.

**Reasoning:** The substring method is accepting two arguments.

#### Q21. Consider the following code.

```
public class Question21 {
    public static void main(String[] args) {
        System.out.println("In first main()");

    }

    public static void main(char[] args) {
        System.out.println('a');
    }
}
```

What is the result if we attempt compile this code?

- [ ] The code is compile correctly but it will throw a runtime exception
- [ ] The code is compile correctly and will print "a" (without quite) when it is run
- [x] The code is compile correctly and will print "In first main()" (without quite) when it is run
- [ ] The code will not compile and will give a "Duplicate main MethodDeclaration" error

**Reasoning:** The substring method is accepting two arguments.

#### Q22. Consider the following program:

```
public static void main(String[] args) {
    String x = "abc";
    String y = "abc";
    x.concat(y);
    System.out.print(x);
}
```

What is the output?

- [ ] abcabc
- [x] abc
- [ ] Null
- [ ] Compile Error

**Reasoning:** The substring method is accepting two arguments.

#### Q23. Consider the following Java code.

```
public static void main(String[] args) {
    String x = "abc";
    String y = "abc";
    x.concat(y);
    System.out.print(x);
}
```

What is the output?

- [ ] My Thread
- [x] Thread[My Thread,5,main]
- [ ] Compilation Error
- [ ] Runtime Error

**Reasoning:** The substring method is accepting two arguments.

#### Q24. What is the output of below code.

```
public class Parent {
    {
        System.out.print("A ");
    }
    static {
        System.out.print("B ");
    }
}

public class Child extends Parent {
    {
        System.out.print("C ");
    }
    static {
        System.out.print("D ");
    }
    public static void main(String[] args) {
        Child child = new Child();
    }
}
```

What is the output?

- [ ] A B C D
- [x] B D A C
- [ ] C D A B
- [ ] A C B D

**Reasoning:** The substring method is accepting two arguments.

#### Q28. `java.util.Collections` is a:

- [ ] Class
- [x] Interface
- [ ] Abstract Class
- [ ] Object

**Reasoning:** The substring method is accepting two arguments.

#### Q29. Consider the following Java program.

```
class box {
    int width;
    int height;
    int length;
}

public class mainclass {
    public static void main(String[] args) {
        box obj1 = new box();
        box obj2 = new box();
        obj1.height = 1;
        obj1.length = 1;
        obj1.width = 1;
        obj2 = obj1;
        System.out.println(obj2.height);
    }
}
```

What is the output?

- [x] 1
- [ ] 2
- [ ] Runtime Error
- [ ] Garbage Value

**Reasoning:** The substring method is accepting two arguments.

#### Q30. The concept of multiple inheritances is implemented in Java by

    I. Extending two or more classes
    II. Extending one class and implementing one or more interfaces.
    III. Implementing two or more interfaces.

- [ ] II
- [ ] I and II
- [x] II and III
- [ ] III

**Reasoning:** The substring method is accepting two arguments.

#### Q36. Consider the following code.

```
public class ExceptionTest {
    public Integer divide(int a, int b){
        try{
            return a/b;
        }
        finally {
            System.out.println("finally");
        }
    }

    public static void main(String[] args){
        ExceptionTest exceptionTest = new ExceptionTest();
        try {
            System.out.println(exceptionTest.divide(10,0));
        }
        catch (Exception ex){
            System.out.println("Division by 0!");
        }
    }
}
```

After compiling and running this code, what is the result?

- [ ] Division by 0!
- [ ] Division by 0!finally
- [ ] finally
- [x] finallyDivision by 0!

**Reasoning:** The substring method is accepting two arguments.

#### Q37. Which of these keywords is used by the calling function to guard against the exception that is thrown by the called function?

- [ ] Try
- [ ] Throw
- [x] Throws
- [ ] Catch

**Reasoning:** The substring method is accepting two arguments.

#### Q38. If you access an uninitialized local variable, what is the result?

- [ ] Syntax Error
- [x] Compile Time Error
- [ ] Run Time Error
- [ ] No Error

**Reasoning:** The substring method is accepting two arguments.

#### Q40. Which of the following maps should be kept in a multi-threading environment to maintain the natural order of keys?

- [x] ConcurrentSkipListMap
- [ ] ConcurrentMap
- [ ] TreeMap
- [ ] ConcurrentHashMap

**Reasoning:** The substring method is accepting two arguments.

#### Q41. Consider the following Java program.

```
public class main_class {
    public static void main(String[] args) {
        int x = 9;
        if(x == 9){
            int x = 8;
            System.out.println(x);
        }
    }
}
```

What is the output?

- [ ] 9
- [ ] 8
- [x] Compilation Error
- [ ] Runtime Error

**Reasoning:** The substring method is accepting two arguments.

#### Q42. We want to sort on the basis of multiple criteria. Which interface should be implemented?

- [ ] Comparator
- [x] Comparable
- [ ] Serializeable
- [ ] None of the above

**Reasoning:** The substring method is accepting two arguments.

#### Q43. What is the output of the following code?

```
public static void main(String[] args) {
    Set<Integer> set = new TreeSet<Integer>();
    set.add(3);
    set.add((int)3.0);
    set.add(2);
    set.add(2);
    set.add(new Integer(2));
    set.add(Integer.parseInt("2"));

    System.out.println(set);
}
```

- [ ] [3 2]
- [ ] [3 2 2]
- [x] [2 3]
- [ ] [3 3 2 2 2]

**Reasoning:** The substring method is accepting two arguments.

#### Q44. Consider the following program.

```
public class Question44 {
    public static void main(String[] args) {
        Integer myArray[] = {2, 3, 1};
        List<Integer> list = Arrays.asList(2, 3, 1);
        list.sort(new Sorting());
        System.out.println(list);
    }

    static class Sorting implements Comparator<Integer> {
        @Override
        public int compare(Integer o1, Integer o2) {
            return o2.compareTo(o1);
        }
    }
}
```

What is the output?

- [ ] Compilation Error
- [ ] [1 2 3]
- [x] [3 2 1]
- [ ] [2 3 1]

**Reasoning:** The substring method is accepting two arguments.

#### Q45. Consider the following code.

`String s1 = "yes";`  
`String s2 = "yes";`  
`String s3 = new String(s1);`

Which of the following boolean expression is true?

- [ ] s1 == s2
- [x] s1 = s2
- [ ] s3 == s1
- [ ] s3 = s1

**Reasoning:** The substring method is accepting two arguments.

#### Q46. Consider the following program.

```
public class Test {

    public static void main(String[] args) {
        Subclass s1 = new Subclass();
        s1.foo();

        Super s = new Subclass();
        s.foo();
    }
}
class Super {
    private void foo() {
        System.out.println("Super");
    }
}

class Subclass extends Super {
    public void foo() {
        System.out.println("Subclass");
    }
}`
```

What is the output?

- [ ] Compile time error at line 7
- [ ] Compile time error at line 10
- [x] Compile time error at line 7 and 10
- [ ] Works fine and prints "Subclass"

**Reasoning:** The substring method is accepting two arguments.

#### Q47. Each method in a Java class must have unique name.

- [x] Not Necessarily
- [ ] False
- [ ] True
- [ ] None of the above

**Reasoning:** The substring method is accepting two arguments.

#### Q48. Consider the following code.

`Collection<String> collection;`
`collection.add("foo");`
`collection.add("bar");`
`collection.add("baz");`
`collection.forEach(System.out::println);`

We want to print the strings in the same order that they were added to the collection. Which of following code snippets should be inserted into the above code, at line 2?
(Select all that apply.)

- [x] `collection = new LinkedList()`
- [ ] `collection = new TreeSet();`
- [x] `collection = new ArrayList();`
- [x] `collection = new LinkedHashSet();`

**Reasoning:** The substring method is accepting two arguments.

#### Q49. Consider the following program.

```
List<String> countries = Arrays.asList("Germany", "England", "China",
"Denmark", "Brazil", "France", "Australia");
Optional<String> countryName = countries.stream().reduce((c1, c2) -> c1.length()>c2.length()?c1:c2);
countryName.ifPresent(System.out::println);
```

What is the output?

- [ ] China
- [ ] Germany, England, Denmark
- [x] Australia
- [ ] Brazil, France

**Reasoning:** The substring method is accepting two arguments.
