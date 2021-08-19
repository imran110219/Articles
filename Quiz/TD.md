## Java

#### Q1. Variables declared as ....... cannot exist on a per-instance basis.

- [ ] Static
- [x] Final
- [ ] Abstract
- [ ] Code

**Reasoning:** The substring method is accepting two arguments.

#### Q20. What will happen if we call the `run()` method instead of calling the `start()` method when starting a thread?

- [ ] Each thread starts in a seperate call stack.
- [x] If we invoke the run() method  from the main thread, run() method will go on to the current call stack rather than going to the begining of a new call stack.
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

#### Q47. Each method in a Java class must have unique name.

- [ ] Not Necessarily
- [x] Flase
- [ ] True
- [ ] None of the above

**Reasoning:** The substring method is accepting two arguments.