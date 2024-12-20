
# I. Getting started
## 4. Why we need tests

**What are software tests**
- code that runs other code and makes assertions and checks
- tests are requirements/specifications
- what is a unit?
	- Method
	- Class
	- Module
- Types of software tests: **unit, integration, end-to-end**

**Why we need automated tests?**
- peace of mind
- catch bugs early
- unit tests impose high code quality
- prevent endless manual tests
- Think big: a TODO list doesn't need tests, a big application probably does


# II. Basics of testing with Jest
## 7. Jest introduction
- jest is a JS/TS testing framework developed by Facebook
- a test runner
- a suit of global functions
- assertion library
- most popular testing framework, most complex solution

## 9. Structure of the unit test
- AAA principle
	- arrange
	- act
	- assert
	- + setup / teardown

```jsx
import { toUpperCase } from "../app/Utils";

describe("Utils test suite", () => {
  test("it should return uppercase of valid string", () => {
    // arrange:
    const sut = toUpperCase; // convention
    const expected = "ABC";
    // act
    const actual = toUpperCase("abc");
    // assert
    expect(actual).toBe(expected);
  });
});
```

## 10. Jest Matchers
- set of functions which compare actual and expected objects
- you can use `it.only('....` to run only one test in the suite.
- `.toBe()` should be used with primitive types
- `.toEqual()` should be used with objects
- objects should be compared with `toEqual(` instead of `to.Be(`
- use `.toHaveLength()` for text length
- `.toContain` - expect array to contain an element
- `.arrayContaining()` - expect array to contain a subarray
- `.not` - to negate assertion
- `.toBeUndefined()`
- `.toBeDefined()`
- `.toBeTruthy()`
- `.toBeFalsy()`


## 11. Multiple tests structure
- you can nest test suits
- each test should be independent

## 12. Parametrized tests
```ts
  describe("ToUpperCase examples", () => {
    it.each([
      { input: "abc", expected: "ABC" },
      { input: "My-String", expected: "MY-STRING" },
      { input: "def", expected: "DEF" },
    ])("$input toUpperCase should be $expected", ({ input, expected }) => {
      const actual = toUpperCase(input);
      expect(actual).toBe(expected);
    });
  });
```

# III. Intermediate testing topics
## 14. F.I.R.S.T principle
- Fast
	- faster tests, faster feedback
- Independent
	- no shared state with other tests
	- the order should not matter
- Repeatable
	- same result with the same input
	- test that writes to a database should always clean up
- Self-validating
	- after the test is finished, it's result should be clear
- Thorough
	- cover all the cases/paths/scenarios
	- happy cases, bad cases, edge cases
	- invalid output
	- large values
	- 100% code coverage is not a great indicator

## 15. Jest Hooks
- `beforeEach`, `afterEach`
- `beforeAll`, `afterAll`

## 17. Jest aliases and watch mode
- `.only` / `.fit`
- `.skip` / `.xit`
- `.concurent` - currently experimental
- `.todo`
	- great way to make a skeleton of a testing application
- you can add `--watch` param to the CLI to get hot reload


## 18. Debug for VSCode
	- search for **vscode recipes** and find jest

launch.js
```js
{
  // Use IntelliSense to learn about possible attributes.
  // Hover to view descriptions of existing attributes.
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "Jest Current File",
      "program": "${workspaceFolder}/node_modules/.bin/jest",
      "args": [
        "--runTestsByPath",
        "${relativeFile}",
        "--config",
        "jest.config.ts"
      ],
      "console": "integratedTerminal",
      "internalConsoleOptions": "neverOpen",
      "disableOptimisticBPs": true,
      "windows": {
        "program": "${workspaceFolder}/node_modules/jest/bin/jest"
      }
    }
  ]
}
```

## 19. Code coverage
- jest uses **istanbul** library by default
- you can also ignore functions from coverage by typing `/* istanbul ignore next */` comment
```jsx
// Jest.config.ts
import type { Config } from "@jest/types";

const config: Config.InitialOptions = {
  preset: "ts-jest",
  testEnvironment: "node",
  verbose: true,
  collectCoverage: true,
  collectCoverageFrom: ["<rootDir>/src/app/**/*.ts"],
};

export default config;
```

# IV. Test Driven Development with Jest and TS

## 21. TDD
- we write our tests first, implementation second
- its good when you want to extend an existing app or fix bugs

## V. Test doubles

## 26. Why do we need test doubles
- some units aren't fast or accessible
	- e.g. database
- replace them in tests
- **pretend objects used in place of real object for testing purposes**
	- **dummy objects**: passed around but not used
	- **fakes**: simplified working implementation, takes a shortcut
	- **stubs:** incomplete objects used as arguments
	- **spies**: tracks information about how a unit is called
	- **mocks:** preprogrammed with expectations
		- most used, most debated

## 28. Stubs
- just incomplete data, you can use `as any` to work around the incompletions

## 31. Mocks
```jsx
  // 1st way to use mocks - jest
  describe("Tracking callbacks with jest mocks", () => {
    const callbackMock = jest.fn();

    afterEach(() => {
      jest.clearAllMocks();
    });

    it("calls callback for invalid argument - track calls", () => {
      const actual = toUpperCaseWithCb("", callbackMock);
      expect(actual).toBeUndefined();
      expect(callbackMock).toHaveBeenCalledWith("Invalid argument!");
      expect(callbackMock).toHaveBeenCalledTimes(1);
    });

    it("calls callback for valid argument - track calls", () => {
      const actual = toUpperCaseWithCb("abc", callbackMock);
      expect(actual).toBe("ABC");
      expect(callbackMock).toHaveBeenCalledWith("called function with abc");
      expect(callbackMock).toHaveBeenCalledTimes(1);
    });
  });

  // 2nd way to use mocks - manual
  describe("Tracking callbacks", () => {
    let cbArgs = [];
    let timesCalled = 0;

    const callbackMock = (arg: string) => {
      cbArgs.push(arg);
      timesCalled++;
    };

    afterEach(() => {
      // clearing tracking fields
      cbArgs = [];
      timesCalled = 0;
    });

    it("calls callback for invalid argument - track calls", () => {
      const actual = toUpperCaseWithCb("", callbackMock);
      expect(actual).toBeUndefined();
      expect(cbArgs).toContain("Invalid argument!");
      expect(timesCalled).toBe(1);
    });

    it("calls callback for valid argument - track calls", () => {
      const actual = toUpperCaseWithCb("abc", callbackMock);
      expect(actual).toBe("ABC");
      expect(cbArgs).toContain("called function with abc");
      expect(timesCalled).toBe(1);
    });
  });
```

## 32. Spies
- spies are not directly injected into SUT
- original functionality is preserved
- spies usually track method calls

```jsx
describe("OtherStringUtils tests with spies", () => {
    let sut: OtherStringUtils;

    beforeEach(() => {
      sut = new OtherStringUtils();
    });

    test("Use a spy to track calls", () => {
      const toUpperCaseSpy = jest.spyOn(sut, "toUpperCase");
      sut.toUpperCase("asa");
      expect(toUpperCaseSpy).toHaveBeenCalledWith("asa");
    });

    test("Use a spy to track calls to other module", () => {
      const consoleLogSpy = jest.spyOn(console, "log");
      sut.logString("abc");
      expect(consoleLogSpy).toHaveBeenCalledWith("abc");
    });

    test("Use a spy to reoplace the implementation of the method", () => {
      jest.spyOn(sut, "callExternalService").mockImplementation(() => {
        console.log("calling mock implementation");
      }); // work around private methods

      sut.callExternalService();
    });
  });
```

## 33. Mocking modules
```jsx
// preserves all other functions but mocks calculateComplexity;
jest.mock("../../app/doubles/OtherUtils.ts", () => ({
  ...jest.requireActual("../../app/doubles/OtherUtils.ts"),
  calculateComplexity: () => 10,
}));

// mock uui module
jest.mock("uuid", () => ({
  v4: () => "123",
}));

import * as OtherUtils from "../../app/doubles/OtherUtils";

describe.only("module tests", () => {
  test("calculate complexity", () => {
    const result = OtherUtils.calculateComplexity({} as any);
    expect(result).toBe(10);
  });

  test("keep other functions", () => {
    const result = OtherUtils.toUpperCase("abc");
    expect(result).toBe("ABC");
  });

  test("string with id", () => {
    const result = OtherUtils.toLowerCaseWithId("ABC");
    expect(result).toBe("abc123");
  });
});

```


# VI. Test doubles in practice
- TDD styles/schools: **London** and **Chicago**
- understand the difference between styles
	- what is a unit?
	- **Chicago**
		- collection of pieces
		- test from a broader view
		- little use of mocks
	- **London**
		- heavy use of mocks
		- unit is a class
		- mock all dependencies
	- **Temperate**
		- unit is a requirement


# X. React unit testing with jest

```jsx
/* eslint-disable testing-library/no-unnecessary-act */
/* eslint-disable testing-library/no-node-access */
import { act, fireEvent, render, screen } from "@testing-library/react";
import LoginComponent from "./LoginComponent";
import user from "@testing-library/user-event";

describe("Login component tests", () => {
  const loginServiceMock = {
    login: jest.fn(),
  };

  const setTokenMock = jest.fn();

  let container: HTMLElement;

  const setup = () => {
    container = render(
      <LoginComponent loginService={loginServiceMock} setToken={setTokenMock} />
    ).container;
  };

  beforeEach(() => {
    setup();
  });

  it("should render the login component", () => {
    const mainElement = screen.getByRole("main");
    expect(mainElement).toBeInTheDocument();
    expect(screen.queryByTestId("resultLabel")).not.toBeInTheDocument();
  });

  it("should render correctly query by testId", () => {
    const inputs = screen.getAllByTestId("input");
    expect(inputs).toHaveLength(3);
    expect(inputs[0].getAttribute("value")).toBe("");
    expect(inputs[1].getAttribute("value")).toBe("");
    expect(inputs[2].getAttribute("value")).toBe("Login");
  });

  it("should render correctly - query by document query", () => {
    const inputs = container.querySelectorAll("input");
    expect(inputs).toHaveLength(3);
    expect(inputs[0].getAttribute("value")).toBe("");
    expect(inputs[1].getAttribute("value")).toBe("");
    expect(inputs[2].getAttribute("value")).toBe("Login");
  });

  it("click login button with incomplete credentials - show required message", () => {
    const inputs = container.querySelectorAll("input");
    const loginButton = inputs[2];

    fireEvent.click(loginButton);
    const resultLabel = screen.getByTestId("resultLabel");
    expect(resultLabel.textContent).toBe("UserName and password required!");
  });

  it("click login button with incomplete credentials - show required message - with user click", () => {
    const inputs = container.querySelectorAll("input");
    const loginButton = inputs[2];

    act(() => {
      user.click(loginButton);
    });

    const resultLabel = screen.getByTestId("resultLabel");
    expect(resultLabel.textContent).toBe("UserName and password required!");
  });

  it("right credentilas - successful login", async () => {
    loginServiceMock.login.mockResolvedValueOnce("123");

    const inputs = container.querySelectorAll("input");

    const userNameInput = inputs[0];
    const passwordInput = inputs[1];
    const loginButton = inputs[2];

    fireEvent.change(userNameInput, { target: { value: "someUser" } });
    fireEvent.change(passwordInput, { target: { value: "somePassword" } });
    fireEvent.click(loginButton);

    expect(loginServiceMock.login).toBeCalledWith("someUser", "somePassword");

    const reultsLabel = await screen.findByTestId("resultLabel");
    expect(reultsLabel.textContent).toBe("successful login");
  });

  it("right credentilas - successful login - with user calls", async () => {
    loginServiceMock.login.mockResolvedValueOnce("123");

    const inputs = container.querySelectorAll("input");

    const userNameInput = inputs[0];
    const passwordInput = inputs[1];
    const loginButton = inputs[2];

    act(() => {
      user.click(userNameInput);
      user.keyboard("someUser");

      user.click(passwordInput);
      user.keyboard("somePassword");

      user.click(loginButton);
    });

    expect(loginServiceMock.login).toBeCalledWith("someUser", "somePassword");

    const reultsLabel = await screen.findByTestId("resultLabel");
    expect(reultsLabel.textContent).toBe("successful login");
  });

  it("wrong credentilas - unsuccessful login", async () => {
    loginServiceMock.login.mockResolvedValueOnce(undefined);

    const inputs = container.querySelectorAll("input");

    const userNameInput = inputs[0];
    const passwordInput = inputs[1];
    const loginButton = inputs[2];

    act(() => {
      user.click(userNameInput);
      user.keyboard("someUser");

      user.click(passwordInput);
      user.keyboard("somePassword");

      user.click(loginButton);
    });

    expect(loginServiceMock.login).toBeCalledWith("someUser", "somePassword");

    const reultsLabel = await screen.findByTestId("resultLabel");
    expect(reultsLabel.textContent).toBe("invalid credentials");
  });
});

```