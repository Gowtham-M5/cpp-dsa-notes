# C++ Basic Syntax and Data Types

## 1. Basic structure of a C++ program

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!";
    return 0;
}
```

### What each part means

- `#include <iostream>`: includes the input/output tools needed for `cout` and `cin`.
- `using namespace std;`: lets us write `cout` instead of `std::cout`. It is convenient for beginner examples, though larger projects may avoid it.
- `int main()`: the main function; program execution starts here.
- `{` and `}`: mark the beginning and end of a block.
- `cout`: prints output.
- `;`: ends a statement.
- `return 0;`: indicates that the program finished successfully.

## 2. Comments

Comments explain code and are ignored by the compiler.

```cpp
// Single-line comment

/*
   Multi-line
   comment
*/
```

## 3. Variables

A variable is a named place used to store a value. Declare it with a data type.

```cpp
int age = 21;
double height = 5.9;
char grade = 'A';
bool isReady = true;
string name = "Gowtham";
```

For `string`, include `#include <string>` (it may be available indirectly through other headers, but explicitly including it is clearer).

A declaration such as `int score;` creates an integer variable. An initialization such as `int score = 90;` gives it an initial value.

## 4. Common data types

| Type | Stores | Example |
|---|---|---|
| `int` | Whole numbers | `int count = 10;` |
| `float` | Decimal values, lower precision than `double` | `float price = 2.5f;` |
| `double` | Decimal values, usually higher precision than `float` | `double pi = 3.14159;` |
| `char` | One character | `char letter = 'G';` |
| `bool` | `true` or `false` | `bool passed = true;` |
| `string` | Text | `string city = "Mysuru";` |

Use double quotes for strings and single quotes for a single character.

## 5. Input and output

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    int age;
    string name;

    cout << "Enter your age: ";
    cin >> age;

    cout << "Enter your name: ";
    cin >> name;

    cout << "Name: " << name << ", age: " << age << '\n';
    return 0;
}
```

- `cin >> variable;` reads input into a variable.
- `cout << value;` prints a value.
- `<<` is used to send values to output; `>>` is used to read input.
- `\n` starts a new line.

Note: `cin >> name` reads only up to whitespace, so a name containing spaces needs a different approach such as `getline`.

## 6. Type awareness

The type controls what kind of value a variable stores and which operations make sense.

```cpp
int a = 7;
int b = 2;

cout << a / b; // 3: integer division discards the fractional part
cout << static_cast<double>(a) / b; // 3.5
```

## Remember

- C++ is case-sensitive: `main`, `Main`, and `MAIN` are different names.
- Most statements end with a semicolon.
- Initialize variables before using their values.
- Match quotes to the kind of data: `'A'` is a character; `"A"` is text.
