# C++ Functions

A function is a named block of code that performs a task. Functions help organize programs, reuse logic, and separate a problem into smaller parts.

## 1. A simple function

```cpp
void greet() {
    cout << "Hello!";
}

int main() {
    greet();
    return 0;
}
```

- `greet` is the function name.
- `void` means the function does not return a value.
- `greet();` calls the function, causing its body to execute.

## 2. Parameters and arguments

Parameters receive values when a function is called; the supplied values are arguments.

```cpp
void greetUser(string name) {
    cout << "Hello, " << name;
}

int main() {
    greetUser("Gowtham");
    return 0;
}
```

Here, `name` is the parameter and `"Gowtham"` is the argument.

## 3. Returning a value

Use a return type such as `int` when a function sends a value back to its caller.

```cpp
int add(int a, int b) {
    return a + b;
}

int main() {
    int result = add(3, 4);
    cout << result; // 7
    return 0;
}
```

- `int` before `add` says the function returns an integer.
- `return a + b;` sends the result back.
- `result = add(3, 4)` stores the returned value.

A non-void function should return a value of the appropriate type on every path that reaches its end.

## 4. `return` exits the function

When a `return` statement executes, the current function ends immediately. Statements after that return in the same execution path are not run.

```cpp
int doubleNumber(int n) {
    return n * 2;
    // Code here would not execute after the return
}
```

## 5. Returning a vector from a function

This is useful for LeetCode problems where the required result is a list of values.

```cpp
#include <iostream>
#include <vector>
using namespace std;

vector<int> getPair() {
    return {2, 5};
}

int main() {
    vector<int> answer = getPair();
    cout << answer[0] << " " << answer[1]; // 2 5
    return 0;
}
```

`return {2, 5};` returns a vector containing the two values. The braces initialize the returned vector; this is not a function call.

In a LeetCode solution such as Two Sum, `return {i, j};` returns the two indices in a `vector<int>`.

## 6. Function declaration / prototype

If a function is defined after `main`, declare it first so the compiler knows its signature.

```cpp
int multiply(int a, int b); // declaration

int main() {
    cout << multiply(3, 4);
    return 0;
}

int multiply(int a, int b) {
    return a * b;
}
```

For small beginner programs, defining the function before `main` is another simple option.

## 7. Why functions matter in DSA

LeetCode often provides a class and a function signature, for example:

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        // logic
        return 0;
    }
};
```

You write the logic inside the required function. The platform calls that method and checks the returned result; you usually do not write your own `main` function for a LeetCode submission.

## Remember

- A function definition describes what it does; a function call runs it.
- Parameters receive inputs.
- A return value sends a result back.
- `void` functions do not return a value.
- `return {i, j};` can return a brace-initialized vector when the function's return type is `vector<int>`.
