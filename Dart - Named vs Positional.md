# Named vs Positional Parameters
In Dart, you can pass arguments to functions and methods in two main ways: using named arguments and positional arguments. These two approaches have different use cases and syntax.

## 1.  Positional Arguments:
-   Passes values to a function or method in the order in which the parameters are defined in the function's parameter list.
-   The order of the arguments is crucial because Dart matches the values passed to the parameters based on their positions.

Example:
```dart
class Person {
  String name;
  int age;

  Person(this.name, this.age);

  @override
  String toString() {
    return 'Person(name: $name, age: $age)';
  }
}

void main() {
  Person person = Person('Aron Cohen', 23);
  print(person);
}
```

## 2.  Named Arguments:
-  Passes values to a function or method by explicitly specifying the parameter names, regardless of their order in the parameter list.
-   Named arguments are particularly useful when a function has many parameters, and you want to make it clear which value corresponds to which parameter.

Example:
```dart
class Person {
  String name;
  int age;

  Person({required this.name, required this.age});

  @override
  String toString() {
    return 'Person(name: $name, age: $age)';
  }
}

void main() {
  Person person = Person(name: 'Aron Cohen', age: 23);
  print(person);
}
```
