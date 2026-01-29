---
filePattern: "**/*.java"
---

Goal: Generate and refactor code following Elegant Objects (EO) principles - a strict object-oriented paradigm that emphasizes immutable, contract-based objects without procedural anti-patterns.

When triggered: When generating new Java code, editing existing Java code, or refactoring Java code.

## Core EO Principles

### What to AVOID (Anti-patterns):
1. **No null** - Never return or accept null; use Optional or Null Object pattern
2. **No code in constructors** - Constructors should only assign parameters to fields
3. **No getters and setters** - Objects should expose behavior, not data
4. **No mutable objects** - All objects must be immutable after creation
5. **No "-er" classes** - Avoid readers, parsers, controllers, sorters, etc.
6. **No static methods** - Not even private static methods; use objects instead
7. **No instanceof/type casting** - No runtime type checking or casting
8. **No public methods without contracts** - Every public method must be declared in an interface
9. **No statements in tests except assertThat** - Test methods should contain only assertions
10. **No ORM/ActiveRecord** - Avoid object-relational mapping frameworks
11. **No implementation inheritance** - Use composition and interfaces instead

### What to DO (Best practices):
1. **Objects over procedures** - Everything is an object with behavior
2. **Contracts first** - Define interfaces before implementations
3. **Immutable by default** - Objects don't change state after creation
4. **Composition over inheritance** - Prefer object composition
5. **Declarative interfaces** - Methods describe what, not how
6. **Small, focused objects** - Single responsibility principle

## Code Style Guidelines

### Class Design:
- Use simple, descriptive names for classes (nouns) and methods (verbs)
- All non-abstract classes must be `final`
- **One class per file** - each public class in its own .java file
- Avoid nested classes; prefer separate top-level classes
- Each class should implement at least one interface
- Keep classes small (under 300 lines)

### Constructor Rules:
- Only one main constructor that initializes all `private final` fields
- Secondary constructors must delegate to main constructor using `this(...)`
- No logic in constructors - only field assignments
- Validate parameters at construction time

### Method Design:
- Minimize local variables; prefer method chaining
- Only one `return` statement per method
- No blank lines inside method bodies
- Methods should be short (under 10 lines ideally)
- Use method chaining: `a.method1().method2()`
- Prefer nested constructors: `new SomeClass(new OtherClass())`

### Interface Design:
- Every public class must implement an interface
- Interfaces define contracts, not implementation details
- Keep interfaces small and focused
- Use default methods sparingly

## Examples

### ❌ BAD (Traditional Java):
```java
public class User {
    private String name;
    private int age;
    
    public User() {}
    
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    
    public int getAge() { return age; }
    public void setAge(int age) { this.age = age; }
    
    public static User createDefault() { return new User(); }
}
```

### ✅ GOOD (EO Style):
```java
public interface User {
    String name();
    int age();
    
    class Smart {
        private final User origin;
        
        public Smart(final User user) {
            this.origin = user;
        }
        
        public boolean isAdult() {
            return this.origin.age() >= 18;
        }
        
        public boolean canVote() {
            return this.origin.age() >= 21;
        }
        
        public String greeting() {
            return String.format("Hello, %s! You are %d years old.", 
                this.origin.name(), this.origin.age());
        }
    }
}

public final class DefaultUser implements User {
    private final String name;
    private final int age;
    
    public DefaultUser(final String name, final int age) {
        this.name = name;
        this.age = age;
    }
    
    @Override
    public String name() { 
        return this.name; 
    }
    
    @Override
    public int age() { 
        return this.age; 
    }
}
```

### Использование:
```java
User user = new DefaultUser("John", 25);
boolean adult = new User.Smart(user).isAdult();
String greeting = new User.Smart(user).greeting();
```

### ❌ BAD (Utility class):
```java
public class StringUtils {
    private StringUtils() {}
    
    public static String capitalize(String str) {
        if (str == null || str.isEmpty()) return str;
        return str.substring(0, 1).toUpperCase() + str.substring(1);
    }
}
```

### ✅ GOOD (EO Object):
```java
public interface Capitalized {
    String value();
}

public final class CapitalizedText implements Capitalized {
    private final String original;
    
    public CapitalizedText(final String original) {
        this.original = original;
    }
    
    @Override
    public String value() {
        return new FirstUpper(this.original).value();
    }
}

public final class FirstUpper implements Capitalized {
    private final String text;
    
    public FirstUpper(final String text) {
        this.text = text;
    }
    
    @Override
    public String value() {
        return this.text.isEmpty() 
            ? this.text 
            : this.text.substring(0, 1).toUpperCase() + this.text.substring(1);
    }
}
```

## Instructions for AI Assistant

1. **Analysis Phase**:
   - Identify EO violations in existing code
   - Check for null usage, getters/setters, static methods, mutable objects
   - Look for classes without interfaces

2. **Refactoring Phase**:
   - Convert data classes to immutable objects with interfaces
   - Replace static methods with object instances
   - Eliminate null by using Optional or Null Object pattern
   - Remove getters/setters, expose behavior instead
   - Make all non-abstract classes `final`

3. **Generation Phase**:
   - Always start with interface definition
   - Implement interface with `final` class
   - Use only one main constructor
   - Make all fields `private final`
   - No logic in constructors
   - Methods return new instances for state changes

4. **Validation Phase**:
   - Verify no EO principles are violated
   - Check all classes implement interfaces
   - Ensure immutability
   - Confirm no static methods or utility classes

## Common Patterns

- **Null Object**: Instead of returning null, return a special object that does nothing
- **Decorator**: Use decorator pattern instead of inheritance
- **Smart Constructor**: Validate input and return validated object
- **Value Object**: Small immutable objects representing values

## Resources
- https://www.yegor256.com - Blog with EO articles
- https://www.elegantobjects.org/ - Official EO website
- https://github.com/yegor256/cactoos - EO collections library
- https://github.com/yegor256/takes - EO web framework
