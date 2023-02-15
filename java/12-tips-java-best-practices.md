# Java best practices tip
## 1. Use clear and intuitive Naming Conventions.

For multiple projects, follow one naming convention in other to maintain uniformity and avoid confusion.
Here are couple tips for setting up easily understandable and clear naming schemes:
- Classes - Names should only include nouns and begin with uppercase letters.
- Packages - Names shuold be entirely written in lowercase.
- Interfaces - Names should follow Camel Case.
- Variables - Names can follow the mixed case convention.
- Methods - Names should consist of verbs with every word capitalized.

After all, a proper naming scheme is even more important than excellent code comments. This is because programmers oftern neglect that part of rheir work and forget to update the comment when changing the code, leading to futher confusion.
## 2. Remember about commenting and writing self-documenting code.
Since we've already mentioned it, let's now move on to one of the most often neglected parts of the software development process - commenting.
How does anyone reading a codebase understand it? First, they need to know what the code is "supposed to do". That's where comments come in.
Commenting is a practice of placing human-readable descriptions inside the code explaining what a particular part of the program is doing. As your code will be read by other team members with varying knowledge of java, comments should give them a clear overview of chosen approaches, and provide additional information that isn't easily understandable just by looking at the code.

> Good comments can greatly simplify java code maintenance, as well as help diagnose and bugs much quicker.

Some developers go even a step futher and make an argument for self-documenting code. This is a kind of code written in a way that doesn't need sparate documentation, as it is virtually self-explanatory to the reader.

Here is an example of an ordinary comment in Java code:

``` java
// check if employee has right to all benefits.
if ((employee.flags && HOURLY_FLAG) && (employee.age > 65))
``` 
Self-documenting code greatly improves overall readability and make your code cleaner.
In this sample a developer can clearly see what is being done:

``` java 
if (employee.isEligibleForFullBenefits()) 
```
Nevertheless, self-documenting code works best in tandem with additional comments that better explain why it is being done.

## 3. Make sure commits are well described.

Code and variables are not the only elements of the software development process which have to be properly describled. The same rule applies the commits as well.

Besides the main content of your code, a commit also stores various additional information like the author of the commit, timestamp, and a message. The latter should not be disregarded, as it provides other team members with valuable information about what was done in the repository over time.

An example of git commit message is:

``` sh
git commit -m "Improve performance with lazy load implementtation for images." 
```

There are a couple of best practices corcerning writing a good commit message that every Java Developer should be familiar with:
- Capitalize the first letter of the commit message, i.e. "Fix bug with global search input deleting user text"
- Keep it brief and straigh to the point. It is generally advised to keep a commit message under 50 characters.
- In your commit messag , focus on what has changed, rather than why you changed it.

## 4. No Empty Catch Blocks.

Java try-catch block is used for handling exceptions. Written code that can throw an exception is placed inside the try-catch block and if a certain exception is thrown, it is handled by the corresponding catch block. So if anything unplained happens in the try block, for instance, divide by zero, file not found, etc. it will generate an exception that is dealt with by the catch block.

In theory, we can have an empty catch block. In reality, though, this is a bad pratice and should be avoided.

> An empty catch block won't give you any information about what went wrong within our code and prolong the bug-fixing process.

Conside the following code snippet:

``` java
public int aggregateIntegerStrings(String[] integers) {
    int sum = 0;
    try {
        for (String integer : integers) {
            sum += Integer.parseInt(integer);
        }
    } catch (NumberFormatException ex) {
    }
    return sum;
}
```

In this exampoole, every catch block is empty and when we run this method with following parameter ["123","1abc"]. The method will fail silently without giving us any feedback and return 123.

Depending on the situation, the code for handling exceptions my be different.

Nevertheless, it is worth remembering to never ignore an exception by creating an empty catch block.

## 5. Proper handling of Null Pointer Exceptions.

NPE or Null Pointer Exceptions is a really common exception in Java.

A NPE is thrown when a program attempts to use an object reference that has a null value. Such a situation can happen when:

- Modifying or accessing a null object's field.
- Invoking a medthod from a null object.
- Modifying or accessing the slots of a null object.
- Throwing null, as if it were a Throwable value.
- Synchronizing over a null object.

Comming across NPE is inevitable when working as a Java software developer, but is is worth following some basic guidelines in order to handle them properly.

> First and foremost, check possible Nulls values and variables prior to code execution so that they can be eliminated. You should also modify your code in orcder to better handle exceptions.

Consider this short code snippet:
```java
int noOfworkers = company.listWorkers().count();
```
Theoretically it shouldn't happen, but if either "Company" or method "listWorkers()" is a Null, the code will throw an NPE.

A better version of this code should look like this:
``` java
private int getListOfWorkers(File[] file) {
    if (file == null) {
        throw new NullPointerException("File list cannot be null");
    }
}
```

## 6. Use StringBuffer or StringBuilder connectiong Strings

A lots of developers regardless of the programming language, write code with the "+" operator to join Strings together. This is true with Java as well.

While not necessarily wrong, using this proves to be inefficient as the java compiler creates multiple intermadiate String objects before creating the final concatenated string. This, in turn, negatively influences the performance.

> Good practice in Java software development is to use "StringBuffer" or "StringBuilder". These built-in functions modify a String without creating intermediate String objects. This save progressing time as well as memory usage.

Consider this code snippet usiong the "+" operator:

``` java
String sql = "Insert Into Users (name, asge)";
sql += " value ('" + user.getName();
sql += "', '" + user.getAge();
sql += "')";
```
Using StringBuilder this code could also be written like this:

``` java
StringBuilder sqlSb = new StringBuilder("Insert Into Users (name, age)");
sqlSb.append(" values ('").append(user.getName());
sqlSb.append("', '").append(user.getAge());
sqlSb.append("')");
String sql = sqlSb.toString();
```
 It is also worth mentioning that in Java 15 we can also use multiline strings (https://www.baeldung.com/java-text-blocks) to greatly improve the readability of such SQL statements.

 ## 7. Use Java libraries ergonomically.

 One of the main reasons why Java still holds the spot as one of the most popular programming languages worldwide is its support the vast variety of the code libraries.

 Known as Java Class Libraries, these sets of pre-written code are essential tools for software architects. Using them, programmer can assemble parts of code faster without the need for writing every single function manually.

 Is is worth nothing, though, that using too many libraries is a bad practice in software programming can prove detrimental in the long run.

 It's because each library requires dedicated system resources to be loaded. Apart from using substantial amounts of system memory, they can also hinder the application's performance. There's also an issue of libraries's quality. Some of them include buggy code which can do more harm than help.

 > Good practice for Java programmers is use only these libraries from trusted sources that fulfill multiple purposes in order to save valuable memory resources.

 ## 8. Class Members must be accessed privately.

 > Java developers should thus use a private modifier to protect the fields in order to enforce information type in the software design.

 Let's consider these public fields:
 ``` java
 public class Employee {
    public String name;
    public int age;
 }
 ```
 Due to the poor software design, field values can be charge inappropriately:

 ``` java
 Employee employee = new Employee();
 employee.name  = "";
 employee.age = 28;
 ```

 Talking into consideration the type of data, these values don't make much sence. A good practice is to hide these fields and allow the code to change them using setter methods or mutators. Here's an example of a better approach:
 ``` java
 public class Student {
    private String name;
    private int age;
    public void setName(String name) {
        if (name == null || name.equals("")) {
            throw new IllegalArgumentException("Name is invalid");
        }
        this.name = name;
    }
    public void setAge(int age) {
        if (age < 1 || age > 100) {
            throw new IllegalArgumentException("Age is invalid");
        }
        this.age = age;
    }
 }
 ```

 ## 9. Avoid redundant initializations.

 Even though this is a pretty common practice among Java developer, we advise against initializing member variables with values: like false, 0, or null.

 These values are already the default initialization values of member variables in Java. It is a good Java best practice to be aware of the default initialization values and avoid initializing other variables.

 ## 10. Avoid memory leaks.

 There are two things that can significantly influence software performance - memory leaks and object creation.

 Generally, Java developers do not have much control over memory management, since Java uses an automatic system for that. While it's cool not to have to worry about freeing and allocating memory manually, it doesn't mean that Java developers should not pay any attention to how memory is used in th application.

 It is a good programming practice to always release database connections after querying, using Finally block as often as possible and releasing instances stored in Static Tables. All of these tips are effective ways of preventing memory leakages.

 There are also a couple of tools to help to detect memory leaks in your code:
 
 - Memory tab in Intellij IDEA: Intellij is one of the most popular IDE in Java development and there's a high chance that you are using it in your everyday work. It also has an in-built feature that allows you to view details of all objects, which is really helpful in detecting memory leaks and their causes.
 - Netbeans Profiler: It can be used to analyze memory usage in Java FX, Java SE, EJB, mobile and web applications.
 - Memory Analyzer (MAT) in Eclipse: It allows Java developers to detect possible memory leakages and easily analyze the heap dump, even if it contains millions of objects.

 ## 11. Float or double?

 Some insufficiently experienced Java programmers have the tendency to use bouble and float in inappropriate applications. They usually choose only one type, regardless of project guidelines.

 If you need precise calculations, you shuold use double instead of float. Most CPU's take a similar amount of time to process operations either on a float or a double, but double value offers much higher precision than float.

 When precision is not as important, a good practice is to use float values instead of double because it takes up half the memory space.

 A good Java developer should always remember that using the right data type significantly improves the performance of your code.

 ## 12. Make suer that the code is well covered with tests.

 Last, but certainly not least, we have to cover software tests.

 Software testing is a method of determining whether the actual software product meets the expected requirements and ensuring that the software product is free of defects. It is often regard as one of the most tiresome chores in software development.\

 But don't neglect it!

 > Code that hasn't been properly covered by tests is notoriously hard to maintain.

A developer may never be sure what part of the project is about to blow up if there is a slight change made to the code.

It is best to strive for the best test coverage possible, but you don't have to go for 80-90% coverage right away. First, focus on the most important ares of the project, and the ones that are most vulnerable to failures and bugs.
