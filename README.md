# OOP Calculator

A command-line calculator built in Python to practice object-oriented programming, testing, error handling, and continuous integration.

The project was developed in stages, beginning with simple calculation objects and gradually adding abstraction, history management, a REPL interface, reliability improvements, and automated testing.

## Features

The calculator supports the following commands:

- `add` — add two numbers
- `subtract` — subtract the second number from the first
- `history` — display calculations from the current session
- `remove` — remove a calculation from history
- `help` — display available commands
- `exit` — exit the calculator

The final version also handles invalid input without crashing, including invalid numbers, invalid history removals, nonfinite numbers, Ctrl+C, and end-of-input.

## Project Structure

```text
my-oop-calculator/
├── calculator/
│   ├── __init__.py
│   ├── __main__.py
│   ├── calculation.py
│   ├── cli.py
│   └── history.py
├── tests/
│   ├── test_calculation.py
│   ├── test_cli.py
│   └── test_history.py
├── .github/
│   └── workflows/
│       └── tests.yml
├── requirements.txt
├── pytest.ini
└── README.md
```

## Installation

Clone the repository:

```bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
cd YOUR-REPOSITORY
```

Create a virtual environment:

```bash
python -m venv .venv
```

Activate it on Linux or WSL:

```bash
source .venv/bin/activate
```

Install the required packages:

```bash
python -m pip install -r requirements.txt
```

## Running the Calculator

Run the calculator from the project root:

```bash
python -m calculator
```

Example session:

```text
OOP Calculator

Type "help" for commands.

> add
First number: 10
Second number: 5
Result: 15

> subtract
First number: 20
Second number: 7
Result: 13

> history
Calculation History

1. Add: 10, 5 = 15
2. Subtract: 20, 7 = 13

> exit
Goodbye!
```

## Running Tests

Run the complete test suite with:

```bash
python -m pytest
```

The final project requires 100% line and branch coverage.

A detailed coverage report can also be generated with:

```bash
python -m pytest --cov-report=term-missing --cov-report=html
```

The HTML report will be created in:

```text
htmlcov/index.html
```

## Design

### Calculation

`Calculation` is an abstract base class that stores two operands and defines the common `get_result()` contract.

`Add` and `Subtract` inherit from `Calculation` and implement their own arithmetic behavior.

This allows different calculation objects to be used through the same interface.

### History

`History` manages a collection of calculation objects.

It is separate from the calculation classes because its responsibility is storing, retrieving, and removing calculations rather than performing arithmetic.

`get_history()` returns a shallow copy so callers cannot directly modify the membership of the internal history list.

### CLI

The CLI is responsible for communicating with the user.

It reads commands, creates the correct calculation object, stores successful calculations in `History`, and displays results.

Object construction and object storage are separate actions.

## Reliability

The calculator handles expected user mistakes without ending the session.

Examples include:

- invalid numeric input
- invalid removal numbers
- nonexistent history entries
- `NaN` and infinity
- arithmetic results outside the supported finite range
- Ctrl+C
- end-of-input

Invalid calculations are not added to history, and unsuccessful removals do not change existing history.

## Testing and Coverage

Tests are divided into calculation, history, and CLI behavior.

Older tests were kept as the project developed so that new changes would not break behavior that already worked.

Coverage helps identify code paths that have not been executed, but coverage alone does not prove that every requirement has been implemented. Assertions are still necessary to verify the expected behavior.

## Continuous Integration

GitHub Actions automatically runs the test suite in a fresh Ubuntu environment.

The workflow tests the project using:

- Python 3.11
- Python 3.12
- Python 3.13
- Python 3.14

The workflow installs the project dependencies and runs pytest with the coverage requirements defined in `pytest.ini`.

## Reflection

### Where would Multiply belong?

I would create a new `Multiply` class that inherits from `Calculation` and implements `get_result()` using multiplication.

I would also add `multiply` to the CLI operations dictionary, include it in the help message, and add tests for multiplication behavior.

`History` would not need any multiplication-specific logic because it only manages `Calculation` objects. The arithmetic remains the responsibility of the calculation subclasses.

### What contract could email and text-message notifications share?

Email and text-message notification objects could share a `send()` method.

Both classes could provide their own implementation of `send()`, while other parts of the program could call the same method without needing to know which notification type is being used.

### What design knowledge transfers to another language?

Concepts such as abstraction, encapsulation, inheritance, polymorphism, separation of responsibilities, testing, and error handling can transfer to other programming languages.

However, I would still need to learn the syntax, type system, libraries, exception handling rules, and runtime behavior of the new language.

## Independent Stage 6 Check

I tested the setup instructions from a fresh clone using a new virtual environment.

If I found an unclear setup instruction, I updated the README so another user could reproduce the project more easily.

If the tests pass but coverage fails in GitHub Actions, I would check the coverage report's `Missing` column. I would identify which line or branch was not executed, determine what behavior should reach that path, and add a meaningful test with an assertion for that behavior.

## Technologies Used

- Python
- pytest
- pytest-cov
- Git
- GitHub
- GitHub Actions
- WSL / Linux

### Where would Multiply belong?

`Multiply` should be another subclass of `Calculation`, just like `Add` and `Subtract`. It would implement its own `get_result()` method. I would also add `multiply` to the CLI operation dictionary, add it to the help text, and create tests for it. `History` would not need multiplication logic because it only stores and manages calculation objects through their shared interface.

### What contract could email and text-message notifications share?

`EmailNotification` and `TextNotification` could both provide a `send()` method. The caller should only need to know that calling `send()` sends the notification, while each class handles the details differently.

### What design knowledge transfers to another language?

Ideas such as abstraction, inheritance, polymorphism, encapsulation, and separating responsibilities transfer to other languages. However, I would still need to learn each language's syntax, type system, inheritance rules, visibility rules, and error handling.