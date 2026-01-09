# Bruhlang Language Specification Dictionary (v0.5.1)

This document is the official reference for the syntax, keywords, and core concepts of Bruhlang. It's the source of truth for the language's vibe.

## Contents
1.  [📜 Program Structure](#-program-structure)
2.  [🤫 Comments](#-comments)
3.  [✨ The Vibe System (Variables & Types)](#-the-vibe-system-variables--types)
4.  [💬 Input & Output](#-input--output)
5.  [🤔 Conditionals](#-conditionals)
6.  [🔁 Loops](#-loops)
7.  [🤙 Functions](#-functions)
8.  [🗿 Error Handling](#-error-handling)
9.  [💥 Panic & Recovery](#-panic--recovery)
10. [💼 Bags, Imports, & Visibility](#-bags-imports--visibility)
11. [🔣 Operators & Logic](#-operators--logic)
12. [Example App](#example-app)
13. [Status of this Document & Legal Notices](#status-of-this-document--legal-notices)

***

## 📜 Program Structure

The basic scaffolding of any Bruhlang script.

| Keyword | Purpose | Example |
| :--- | :--- | :--- |
| `sup` | Kicks off the program. The first word in any script. | `sup` |
| `k bye` | Ends the program. The last line in any script. | `k bye` |

## 🤫 Comments

For when you need to explain something `sus`, whether it's a one-liner or a whole story.

| Syntax | Purpose | Example |
| :--- | :--- | :--- |
| `sus:` | A single-line comment. The compiler ignores the rest of the line. | `sus: this part is tricky, ngl` |
| `sus:{ ... }`| A multi-line comment block. The compiler ignores everything between the braces. Used for long explanations or for temporarily disabling code. | `sus:{ vibe x is now "disabled" }` |

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

### Block Declaration

In addition to single-line declarations, Bruhlang supports a block syntax for declaring a group of related variables or constants. Use the plural `vibes` for a block of variables. The `locked` keyword remains singular as it describes the state of the entire block.

```
vibes (
  name: text is now "Brandon"
  age: num is now 30
  isReady is now facts
)

locked (
  StatusOK: num is now 200
  StatusError: num is now 500
)
```

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

For bundling up code to reuse later. Bruhlang uses a standard `functionName(...)` syntax for all function calls, making the code clean and instantly familiar.

| Keyword | Purpose | Example |
| :--- | :--- | :--- |
| `the function` | Starts the definition of a new function. | `the function doAThing` |
| `takes (...)` | Specifies the parameters a function accepts in its definition. | `takes (num a, text b)` |
| `returns` | Specifies the return type(s). Use `or` for alternative types or `()` for multiple simultaneous types. | `returns text or bruh` <br> `returns (text, bruh)` |
| `yeet` | Returns one or more values from a function. | `yeet facts` <br> `yeet user, err` |

### Multiple Return Values
Bruhlang functions can return multiple values, which is the standard way to handle errors. The return signature can also optionally name the values for documentation purposes, using the standard colon (`:`) annotation.

| Part | Syntax | Example |
| :--- | :--- | :--- |
| **Signature (Unnamed)** | `returns (<type1, type2>)` | `returns (text, bruh)` |
| **Signature (Named)** | `returns (<name1: type1, ...>)` | `returns (user: text, err: bruh)` |
| **Return Action** | `yeet <value1, value2, ...>` | `yeet "Success", ghosted` |
| **Receiving** | `vibes <var1, var2, ...> are now funcName(...)`| `vibes user, err are now getUser(1)`|

**Note:** ***🚫 NO NUDE YEETING.*** Bruhlang requires explicit `yeet`s. "Naked" returns are not allowed. The names provided in a return signature are for **documentation purposes only** and do not change the positional nature of the return values. They cannot be used for named destructuring.

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

***

# Example App

## Welcome to Bruhlang: Your First App
Let's build a simple command-line app that calls a web API. This will show you how Bruhlang handles everything from modern function calls and modules (we call them `bags`) to a full spectrum of error and panic handling.

Our app will have two parts:
1.  **`api-bag.bruh`**: A reusable "bag" of tools for talking to our API.
2.  **`main.bruh`**: Our main app that uses the bag and is built to survive anything the bag throws at it.

### 1. The Library: `api-bag.bruh`
This is our reusable code. We're creating a tool that other scripts can use. We use `highkey` to make our `Get` function public so other bags can `dip into` it.

```
// File: api-bag.bruh
sus: in the 'api-bag'

sup
  highkey the function Get takes (url: text) returns (data: text, errin: bruh)
    fr? (url is "https://api.example.com/vibe")
      sus: Happy path: yeet the good data and a ghosted error.
      yeet "{""data"": ""vibe is immaculate""}", ghosted

    or like, fr? (url is "https://api.example.com/ghosted")
      sus: Predictable error (404 Not Found): yeet empty data and a new bruh.
      yeet "", new bruh with "404: that endpoint is ghosted"

    or like, fr? (url is "https://api.example.com/corrupt")
      sus: Catastrophic failure: The server sent us garbage data.
      sus: This is a ragequit moment for our internal parser.
      ragequit with "internal parser error: malformed data"

    nah
      yeet "", new bruh with "400: bad request"
    aight
  bet
k bye
```

### 2. The Main App: `main.bruh`
This is the script we'll actually run. Because `api-bag.Get` can `ragequit`, we create a "wrapper" function (`safeApiCall`) that acts as a safety harness. It catches any potential panics and turns them into regular `bruh` moments for our app to handle.

```
// File: main.bruh
sup
  dip into 'api-bag'

  sus: This "safe" function calls the risky API but has a safety net.
  the function safeApiCall takes (url: text) returns (text, errin: bruh)
    sus: The 'later' block runs before this function exits, no matter what.
    later
      vibe thePanic is now chill()  sus: 'chill()' catches a ragequit.
      fr? (thePanic is not ghosted)
        sus: If we caught one, turn it into a normal 'bruh' and yeet it.
        yeet "", new bruh with "PANIC CAUGHT: " plus thePanic
      aight
    bet

    sus: We call the function and yeet its results directly.
    yeet api-bag.Get(url)
  bet

  spill "--- Hitting up the API ---"

  sus: We use 'vibes' to catch the multiple return values.
  vibes response, errin are now safeApiCall("https://api.example.com/corrupt")

  sus: Now we check ONLY the 'errin' vibe. Clean "keep left" error handling.
  bruh? (errin)
    spill "--- BRUH MOMENT ---"
    spill "The app caught an error: " plus errin
    k bye  sus: We decided this error is fatal. End the script.
  aight

  spill "--- VIBE CHECK: PASSED ---"
  spill "Success! API Response: " plus response
k bye
```

### Running the App: Three Possible Vibes
By changing the URL in the `safeApiCall` in `main.bruh`, you can see all three paths.

**1. The Happy Path (URL: `"https://api.example.com/vibe"`)**
> --- Hitting up the API ---
> --- VIBE CHECK: PASSED ---
> Success! API Response: {"data": "vibe is immaculate"}

**2. The Bruh Moment (URL: `"https://api.example.com/ghosted"`)**
> --- Hitting up the API ---
> --- BRUH MOMENT ---
> The app caught an error: 404: that endpoint is ghosted

**3. The `ragequit` (URL: `"https://api.example.com/corrupt"`)**
> --- Hitting up the API ---
> --- BRUH MOMENT ---
> The app caught an error: PANIC CAUGHT: internal parser error: malformed data

### The Vibe Explained: What You Just Saw
This simple app shows off the core of Bruhlang:

*   **Explicit Error Handling:** We use multiple return values (`returns (data: text, errin: bruh)`) as the standard way to handle predictable errors. `errin` is the conventional name for error vibes.
*   **Resilience (`ragequit`/`chill`):** Bruhlang is built to survive a catastrophe. Our app can "catch" a `ragequit` from a dependency and turn it into a manageable `bruh` moment, preventing a crash.
*   **Chilled Out Slappin' Vibe:** While Bruhlang (aka "bruh" for those who know...) is pulls its vibe from the highly prescriptive no-nonsense simplicity of Go, a significant amount of boiler plate and cold syntax of The Ancient Arts has been chilled out.
*   **Natural Language Flow:** Bruh is meant to feel natural, like a conversation, or vibing an explicit instruction set to a no cap based bruh. Symbols from the traditional languages of The Ancient Arts are mere relics here, and used only when they enhance readability, and optionally (i.e. in the case of math operators) at a bruh's discretion when the vibe needs to hit different. 

It's a language designed from the ground up to be both fun to write and seriously safe to run.

## Status of this Document & Legal Notices
This is an early soft-release spec that is being made available for feedback, input, and to guage interest level for contributing. Other parties may have some claim to this but the intent is to discuss the best licensing option as a community of contributors once such a degree of community interest is established. Please contact the repository owner @BHunter2889 for guaging interest, who may also be reached on Discord: @dadderall_42mg.

Copyright © 2025-2026 Brandon Hunter and Bruhlang contributors. All rights reserved.
