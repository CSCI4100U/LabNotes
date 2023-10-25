# Handling Variables
In Dart, you have several options for handling and declaring variables. Here's a breakdown of when to use each:

## 1. `late`:
-   Use `late` when you know that a variable will have a value assigned to it before you access it, but you can't provide an initial value at the time of declaration.
-   It's often used when you need to initialize the variable in a constructor or an init method.

Example:
```dart
class Person {
  late String name;
  late int age;

  @override
  String toString() {
    return 'Person(name: $name, age: $age)';
  }
}

void main() {
  Person person = Person();
  person.name = 'Aron Cohen';
  print(person.name); // Outputs: 'Aron Cohen'
  print(person); // Throws Error as field `age` has no data.
}
```
## 2. `required`:

-   Use `required` for parameters in constructors or functions when you want to ensure that a value is provided when an instance or function is created/called. This is used for non-nullable parameters.

Example:
```dart
class Person {
  String name;
  int age;

  // Note the Named Parameters usage using {}
  Person({required this.name, required this.age});

  @override
  String toString() {
    return 'Person(name: $name, age: $age)';
  }
}

void main() {
  // Note the direct calls to the named parameter fields
  Person person = Person(name: 'Aron Cohen', age: 23);
  print(person); // Outputs: Person(name: Aron Cohen, age: 23)
}

```
## 3. Initialize default value:

-   Initialize a variable when you want to provide a default value in case no value is explicitly assigned later.

Example:
```dart
class Person {
  String name;
  int age;

  Person({this.name = 'N/A', this.age = 0});

  @override
  String toString() {
    return 'Person(name: $name, age: $age)';
  }
}

void main() {
  Person person = Person(name: 'Aron Cohen', age: 23);
  print(person); // Outputs: Person(name: Aron Cohen, age: 23)
  Person person2 = Person();
  print(person2); // Outputs: Person(name: N/A, age: 0)
}
```
## 4. `?` (nullable):

-   Use `?` after a type to indicate that a variable can have a null value. This is helpful when you want to explicitly allow null values.
- Use `!` to assert that a variable is not null. This is called the "non-null assertion operator" or "bang operator."
- If your data should not be null, avoid `?`. It's hard to do operations against a null value.

Example:
```dart
class Person {
  String? name;
  int? age;

  Person({this.name, this.age});

  @override
  String toString() {
    return 'Person(name: $name, age: $age)';
  }
}

void main() {
  Person person = Person();
  print(person); // Outputs: Person(name: null, age: null)
  person.age = person.age! + 1; // Throws Error: Uncaught TypeError: Cannot read properties of null (reading '$add')
}
```

Choosing between these options depends on your program's requirements and design. Here are some general guidelines:

-   Use `late` when you're confident that a value will be assigned before it's accessed, but you can't provide an initial value.
-   Use `required` when you need to ensure a value is provided, especially in constructors and function parameters.
-   Initialize a default value when it makes sense to have a default value in case none is assigned.
-   Use `?` when you explicitly want to allow null values for a variable.


