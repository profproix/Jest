# Unit Testing with Jest

## **Learning Goals**

- [ ] Understand what Jest is and why it is used for automated testing in JavaScript.
- [ ] Install and configure Jest in a project using `npm install` and a `test` script in `package.json`.
- [ ] Write basic test suites with `describe` and individual tests with `test` or `it`.
- [ ] Use Jest matchers such as `toBe`, `toEqual`, and `toThrow` to check different kinds of results.
- [ ] Organize tests so each function is tested for both typical and edge cases.
- [ ] Run tests from the command line with `npm test` and interpret the output to identify failures.

## Node & npm

In the past, JavaScript could only be used inside the browser. When **Node.js** was created, it took JavaScript out of the browser and allowed it to run on our local machines.

With Node comes **npm** (Node Package Manager). This is a tool for installing packages that can be used in JavaScript projects.

Packages are essentially collections of code written by other people so you don't have to write everything from scratch. They handle repetitive or common tasks, so you can focus on other development goals.

npm's package repository holds hundreds of thousands of packages—check it out here: [https://www.npmjs.com/](https://www.npmjs.com/)

### Install Node

If you don't have Node installed yet, follow the instructions here to install it: [https://nodejs.org/](https://nodejs.org/)

## Unit Tests

## Understanding Unit Tests

Unit tests are small, focused tests that check one piece of code at a time.  
They let you verify that each function or module behaves exactly as intended,  
which is especially useful when you’re trying to track down bugs.

### Test Structure

Unit tests are usually organized into:

- **Test suites** – Groups of related tests.
- **Test cases** – Individual checks within a suite. Each case covers one specific scenario.  
  _Example:_ For a calculator’s `add` function, a single test case might confirm that `add(2, 3)` returns `5`.

### What to Test

When writing unit tests, you typically check:

- **Happy path** – The expected, normal behavior.
- **Edge cases** – Unusual inputs or situations that might break your code.

_Example:_ For a calculator’s `divide` function, you’d test normal division (like `divide(10, 2)` equals `5`) and also the edge case of dividing by zero to confirm the code handles it safely.

## Jest

Jest is a **JavaScript testing framework** that provides both a testing environment and built-in methods to create unit tests.

### Structure

- A **`describe` block** groups related test cases together.
- A **`test` block** defines a single test case and ends with one or more **assertions**—statements that check whether the output matches expectations.

### Common Assertion Helpers

- **expect(value).toBe(expected)** – checks strict equality.
- **expect(value).toEqual(expected)** – checks that objects or arrays have the same structure and values.
- **expect(value).toBeTruthy() / toBeFalsy()** – checks if a value is truthy or falsy.
- **expect(value).toContain(item)** – checks that an array or string contains a specific item.
- **expect(() => fn()).toThrow()** – checks that a function throws an error.

Find more here at the JEST docs
[JEST](https://jestjs.io/docs/getting-started)

```
describe("description of the suit", () => {
  test("description of the case", () => {
    //assertions
  });
});
```

## Deliverables

### 1. Install Jest

- **Initialize Node modules**: run npm init with the `-y` flag to quickly create a package.json file.

- **Install Jest as a development dependency**: run npm install with the `--save-dev jest` option.

- **Update the scripts section in package.json**: set the `"test"` script to `"jest"`.

- **Run your tests**: use the command `npm run test`.  
  It’s a good idea to run this as soon as you finish writing your first tests to confirm everything is set up correctly.

### 2. Create a test file for calculator.js

- **Create a test file**: Test files are usually named after the module they test.  
  Since we are testing the functions in **calculator.js**, name the file **calculator.test.js**.

- **Import the functions from calculator.js**:  
   At the bottom of **calculator.js** you’ll see  
   `module.exports = { add, subtract, multiply, divide, calculate };`  
   This allows these functions to be used in other files.

  In **calculator.test.js**, import them with: `const {
  add,
  subtract,
  multiply,
  divide,
  calculate,
} = require("./calculator.js");`

### 3. Create tests for add

- Start by creating a **test suite** using `describe`. Pass it a string that describes the suite and a callback function.

- Inside that callback, call `test`. Pass `test` a string that describes the individual test case.

- Add an **assertion** inside the test case, for example:  
   `expect(add(20, 5)).toBe(25);`
- Verify by running your tests with `npm run test`
  <details>
    <summary>Click Here to view solution</summary>
    ```
    describe("add", () => {
      test("adds two positive numbers", () => {
        expect(add(20, 5)).toBe(25);
      });
    });

  ```
  </details>

  ```

### 4. Add more test cases

- Add a test case to check that adding negative numbers works correctly.

- Add a test case to check the result when adding 0 to another number.
- Verify by running your tests with `npm run test`
  <details>
    <summary>Click Here to view solution</summary>

```
      describe("add", () => {
        test("adds two positive numbers", () => {
          expect(add(20, 5)).toBe(25);
        });

        test("adds a negative and a positive number", () => {
          expect(add(-4, 7)).toBe(3);
          });

        test("adds zero to a positive number", () => {
          expect(add(0, 12)).toBe(12);
        });

```

  </details>

### 5. Repeat for each function from calculator.js

- Verify by running your tests with `npm run test`

  <details>
  <summary>Click Here to view solution</summary>

```
    // subtract
    describe("subtract", () => {
      test("subtracts a smaller number from a larger one", () => {
        expect(subtract(15, 6)).toBe(9);
      });

      test("subtracts a negative number from a positive", () => {
        expect(subtract(10, -5)).toBe(15);
      });
    });

    // multiply
    describe("multiply", () => {
      test("multiplies two positive numbers", () => {
        expect(multiply(4, 6)).toBe(24);
      });

      test("multiplies a negative and a positive number", () => {
        expect(multiply(-3, 5)).toBe(-15);
      });
    });

    // divide
    describe("divide", () => {
      test("divides a larger number by a smaller one", () => {
        expect(divide(20, 4)).toBe(5);
      });

      test("returns an error when dividing by zero", () => {
        expect(divide(12, 0)).toBe("Cannot divide by zero");
      });

      test("divides a negative number by a positive number", () => {
        expect(divide(-12, 4)).toBe(-3);
      });
    });

    // calculate
    describe("calculate", () => {
      test("handles addition operator", () => {
        expect(calculate(14, "+", 6)).toBe(20);
      });

      test("handles subtraction operator", () => {
        expect(calculate(20, "-", 8)).toBe(12);
      });

      test("handles multiplication operator", () => {
        expect(calculate(5, "*", 5)).toBe(25);
      });

      test("handles division operator", () => {
        expect(calculate(18, "/", 3)).toBe(6);
      });

      test("handles divide by zero in calculate", () => {
        expect(calculate(9, "/", 0)).toBe("Cannot divide by zero");
      });

      test("returns unknown operator message", () => {
        expect(calculate(2, "%", 3)).toBe("Unknown operator");
      });
    });

```

  </details>
