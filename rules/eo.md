---
filePattern: "**/*.java"
---

Goal: Follow the principles of Elegant Objects.

When triggered: When you generate or edit code.
Links:
- https://www.yegor256.com
- https://www.elegantobjects.org/

EO principles:
- No null
- No code in constructors
- No getters and setters
- No mutable objects
- No readers, parsers, controllers, sorters, and so on
- No static methods, not even private ones
- No instanceof, type casting, or reflection
- No public methods without a contract (interface)
- No statements in test methods except assertThat
- No ORM or ActiveRecord
- No implementation inheritance

CodeStyle:
- Use simple names for classes and fields
- All non-abstract classes have the final modifier
- Prefer not write nested classes 
- Only one main constructor initialize private fields, other constructor use main (this(a,b))
- Minimize local variable usage, use code explicitly without local variables
- Prefer call code nested constructors (like new SomeClass(new OtherClass())) or stream api style a.method1().method2()
- Use only one return statement in method
- No blank lines in method body

Instructions: 
- Generate, write or refactor the code so that it follows the EO principles
- Review code you written to follow EO principles and CodeStyle
