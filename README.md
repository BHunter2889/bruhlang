# Bruhlang Language Specification Dictionary (v0.4.1)

This document is the official reference for the syntax, keywords, and core concepts of Bruhlang. It's the source of truth for the language's vibe.

## 📜 Program Structure

The basic scaffolding of any Bruhlang script.

| Keyword | Purpose | Example |
| :--- | :--- | :--- |
| `sup` | Kicks off the program. The first word in any script. | `sup` |
| `k bye` | Ends the program. The last line in any script. | `k bye` |

## 🤫 Comments

For when you need to explain something `sus`.

| Syntax | Purpose | Example |
| :--- | :--- | :--- |
| `sus:` | A single-line comment. The compiler will ignore this line. | `sus: this part is tricky, ngl` |

## ✨ The Vibe System (Variables & Types)

The core system for creating, checking, and changing variables. Strong vibes only bruh.

### Variable Declaration
Declaration is done using the `vibe` keyword. Use a colon (`:`) to provide an explicit type annotation.

| Declaration Style | Syntax | Purpose |
| :--- | :--- | :--- |
| **Type Inference** | `vibe <name> is now <value>` | Declares a variable and infers its type from the initial value. This is the most common style. |
| **Type-Only** | `vibe <name>: <type>` | Declares a variable with a specific type, initialized to `ghosted`. |
| **Explicit Type & Value** | `vibe <name>: <type> is now <value>` | Declares a variable with an explicit type and an initial value, for maximum clarity. |

### Constants
For values that should never change.

| Keyword | Purpose | Example |
| :--- | :--- | :--- |
| `locked` | Declares a constant (an immutable variable). Its value cannot be changed. | `locked URL is now "https://example.com"` |

### Type Checking
To check a variable's type, use the `clock` operator within a conditional. This is a read-only action that identifies the variable's current type.

| Syntax | Purpose | Example |
| :--- | :--- | :--- |
| `clock <variable> is <type>` | Evaluates to `facts` or `cap` based on the variable's type. | `fr? (clock userAge is num)` |

### Type Conversion (Casting)
To safely convert a variable to a new type. This is an action that creates a new value.

| Syntax | Purpose | Example |
| :--- | :--- | :--- |
| `vibe check <var> as <type>`| Casts a variable to a new type. Returns `ghosted` if the cast fails. | `vibe myNum is now (vibe check "42" as num)` |

### Built-in Types

| Type | Vibe |
| :--- | :--- |
| `num` | For any numbers, integer or float. |
| `text` | For strings of text. |
| `truth` | For boolean values (`facts` or `cap`). |
| `bruh` | The built-in error type. |
| `ghosted` | The equivalent of null or nil. Represents the absence of a value. |

## 💬 Input & Output

How the script talks to the user.

| Keyword | Purpose | Example |
| :--- | :--- | :--- |
| `spill` | Prints a value to the console. | `spill "Hello, world!"` |
| `listen_up` | Reads input from the user from the console. | `vibe userInput is now listen_up` |

## 🤔 Conditionals

For when you need to make decisions.

| Keyword | Purpose | Example |
| :--- | :--- | :--- |
| `fr? (...)` | Starts a conditional block. The "if" statement. | `fr? (x is more than 5)` |
| `or like, fr? (...)` | An "else if" block. Can be chained multiple times. | `or like, fr? (x is 5)` |
| `nah` | The "else" block. Executes if all `fr?` conditions are `cap`. | `nah` |
| `aight` | Closes a conditional block. | `aight` |

## 🔁 Loops

For doing things over and over.

| Construct | Purpose | Example |
| :--- | :--- | :--- |
| `keep it a hunnid i from 1 to 100` | A standard "for" loop that iterates a counter within a range. | `keep it a hunnid i from 1 to 10` |
| `so long as (...)` | A "while" loop. Continues as long as the condition is `facts`. | `so long as (isWorking is facts)` |
| `bet` | Closes any loop block. | `bet` |

## 🤙 Functions

For bundling up code to reuse later.

| Keyword | Purpose | Example |
| :--- | :--- | :--- |
| `the function is` | Defines a new function. | `the function is (doAThing)` |
| `takes (...)` | Specifies the parameters a function accepts. | `takes (num a, text b)` |
| `returns` | Specifies the return type of a function. Can return multiple types for error handling. | `returns text or bruh` |
| `hit up` | Calls a function. | `hit up doAThing` |
| `with (...)` | Passes arguments to the function being called. | `with (10, "yo")` |
| `yeet` | Returns a value from a function. | `yeet facts` |

## 🗿 Error Handling

Bruhlang handles predictable, expected errors with a dedicated `bruh` type and a special conditional block for checking for "bruh moments". The philosophy is to handle errors immediately and keep the main logic path clean ("keep left").

| Keyword | Purpose | Example |
| :--- | :--- | :--- |
| `bruh` | The built-in error type. Functions can return a `bruh` to signal failure. | `the function is (X) returns text or bruh` |
| `new bruh with` | Creates a new `bruh` error value with a descriptive text message. | `yeet new bruh with "that ain't it"` |
| `bruh? (...)` | A special conditional block that executes only if a variable is a `bruh` type. It is used for guard clauses and early returns. | `bruh? (result) ... aight` |

## 💥 Panic & Recovery

For handling unexpected, catastrophic bugs (not for normal errors). This system allows a part of the program to fail and be logged without crashing the entire application.

| Keyword | Purpose | Example |
| :--- | :--- | :--- |
| `later` | Schedules a function call to be executed just before the surrounding function exits, whether normally or during a `ragequit`. | `later hit up cleanup` |
| `ragequit with` | Triggers a panic state with a descriptive **text** message. This signals a critical, unrecoverable bug. | `ragequit with "ran out of memory"` |
| `chill()` | A special built-in function, only for use in `later` blocks. It stops a `ragequit` and returns the `text` value passed to it. If no `ragequit` is happening, it returns `ghosted`. | `vibe reason is now chill()` |

## 💼 Bags, Imports, & Visibility

Bruhlang uses **bags** (packages/modules) to organize and share code across different files. 

**Bag Declaration Convention**

While the directory name syntactically defines the bag, it is a strongly recommended convention to declare which bag a file belongs to for readability. This is done using a `sus:` comment at the very top of the file, *before* the `sup` initializer. This convention will be encouraged by official Bruhlang tooling and linters.

```bruh
sus: in the 'string-bag'

sup
  sus: rest of the code goes here...
```

The system is built on two core concepts: controlling what a bag makes public (visibility) and how another file uses that public code (importing).

### Controlling Visibility
Use `highkey` and `lowkey` to set whether an item (like a function or constant) in a bag is public or private.

| Keyword | Purpose | Example |
| :--- | :--- | :--- |
| `lowkey` | **(Default)** Restricts an item to its own **bag**. It's private and cannot be used by other files. | `lowkey vibe secret is now "shhh"` |
| `highkey`| Makes an item available to other **bags**. It's public and can be imported by other files. | `highkey locked AppVersion is now "1.0"` |

### Using Bags
Once a bag has `highkey` items, you can use them in another file in one of two ways.

#### Full Bag Imports
This method imports the entire bag, requiring you to use the bag's name as a namespace to access its contents. This is useful when you need many items from a bag or want to be explicit about where an item comes from.

| Keyword | Purpose | Example |
| :--- | :--- | :--- |
| `dip into` | Imports an entire **bag**, making its `highkey` items available. | `dip into 'math-bag'` |
| `.` | The accessor. Used to access an item from a bag you've dipped into. | `vibe sum is now math-bag.Add with (2, 2)` |

#### Named Imports
This method pulls specific `highkey` items from a bag directly into your file's scope, allowing you to use them without a namespace. This is useful for grabbing just a few items or for writing more concise code.

| Keyword | Purpose | Example |
| :--- | :--- | :--- |
| `grab` | Imports one or more named items from a bag. | `grab Add, PI from 'math-bag'` |
| `from` | Used with `grab` to specify the source bag. | `grab Add from 'math-bag'` |
| `aka` | Aliases an imported item with a new name to avoid naming conflicts. | `grab Add aka Plus from 'math-bag'` |

## 🔣 Operators & Logic

The words you use to do math and make comparisons.

### Math

| Operator | Purpose |
| :--- | :--- |
| `plus` | Addition |
| `minus` | Subtraction |
| `times` | Multiplication |
| `over` | Division |
| `mod` | Modulo (remainder) |

### Comparison & Logic

| Operator | Purpose |
| :--- | :--- |
| `is` | Equality (`==`) |
| `is not` | Inequality (`!=`) |
| `is more than` | Greater than (`>`) |
| `is less than` | Less than (`<`) |
| `and` | Logical AND |
| `or` | Logical OR |
| `not` | Logical NOT |

### Boolean Values

| Value | Vibe |
| :--- | :--- |
| `facts` | Represents truth. |
| `cap` | Represents falsehood. |

## Status of this Document & Legal Notices
This is an early soft-release spec that is being made available for feedback, input, and to guage interest level for contributing. Other parties may have some claim to this but the intent is to discuss the best licensing option as a community of contributors once such a degree of community interest is established. Please contact the repository owner @BHunter2889 for guaging interest, who may also be reached on Discord: @dadderall_42mg.

Copyright © 2025-2026 Brandon Hunter and Bruhlang contributors. All rights reserved.
