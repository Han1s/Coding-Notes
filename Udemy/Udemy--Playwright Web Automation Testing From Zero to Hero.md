
# I. Preparation

## 2. Playwright vs Cypress
- Playwright
	- Faster
	- JS/TS
	- free parallel execution
	- can handle multiple tabs
	- better with iFrames
	- more comfortable transition from selenium
- Cypress
	- Faster scripting
	- better auto-wait
	- clear docs
	- dashboard service


# II. Playwright Hands-On Overview
- `npx playwright`test` runs test suite
- `npx playwright show report` shows report
- `npx playwright test --projeect=chromium` runs only for chromium
- `npx playwright test --project=chromium --headed` runs with headed
- `npx playwright test example.spec.ts --project=chromium` runs only a specific file
- `npx playwright test -g "has title" --project=chromium` runs only a specific test
- to skip a test:
	```jsx
test.skip('has title', async ({ page }) => {
	await page.goto('https://playwright.dev/');
	
	// Expect a title "to contain" a substring.
	await expect(page).toHaveTitle(/Playwright/);
});
```
- to run a specific test
	```jsx
test.only('has title', async ({ page }) => {
	await page.goto('https://playwright.dev/');
	  
	
	// Expect a title "to contain" a substring.
	await expect(page).toHaveTitle(/Playwright/);
});
```

## 19. Test executon With UI
- for UI you can just use the VS extension
	- it enables filtering browsers, showing head, running particular tests, etc.
- `npx playwright test --ui` runs the UI for tests
	- you can use the watch icon to automatically hot rerun  the test

## 20. Trace View and Debug
- `npx playwright test --project=chromium --trace on`
	- you can then open the report and open traces section
- `npx playwright test --project=chromium --debug`
	- enables debugging
- to use the build-in debugger
	- put a breakpoint and debug in the test explorer (VS extension)

## 21. Test Structure
- for promises use `await` to avoid errors
```ts
import {test} from "@playwright/test";

test("the first test", async ({page}) => {
  await page.goto('http://localhost:4200/');
  await page.getByText('Forms').click();
  await page.getByText('Form Layout').click();
});
```

## 22. Hooks and Flow control

```tsx
test.beforeEach(async ({ page }) => {
  await page.goto("http://localhost:4200/");
  await page.getByText("Forms").click();
});

test("the first test", async ({ page }) => {
  await page.getByText("Form Layout").click();
});

test("navigate to datepicker page", async ({ page }) => {
  await page.getByText("Datepicker").click();
});
```

## 24. Locator Syntax Rules
```ts
test.beforeEach(async ({ page }) => {
  await page.goto("http://localhost:4200/");
  await page.getByText("Forms").click();
  await page.getByText("Form Layouts").click();
});

test("Locator syntax rules", async ({ page }) => {
  // tag name
  await page.locator("input").first().click();

  // ID
  await page.locator("#inputEmail1").click();

  // single class
  page.locator(".shape-rectangle");

  // attribute
  page.locator('[placeholder="Email"]');

  // class value (full)
  page.locator(
    '[class="input-full-width size-medium status-basic shape-rectangle nb-transition"]'
  );

  // combine different selectors
  page.locator('input[placeholder="Email"][nbinput]');

  // XPath (NOT RECOMMENDED)
  page.locator('//*[@id="inputEmail1"]');

  // partial text match
  page.locator(':text("Using")');

  // exact text match
  page.locator(':text-is("Using the Grid")');
});
```

## 25. User-Facing Locators
- tests should test behavior that user sees (e.g. instead of buttonId you should test button text)

```jsx
test("user facing locators", async ({ page }) => {
  await page.getByRole("textbox", { name: "Email" }).first().click();
  await page.getByRole("button", { name: "Sign in" }).first().click();

  await page.getByLabel("Email").first().click();

  await page.getByPlaceholder("Jane Doe").click();

  await page.getByText("Using the Grid").click();

  // not user facing, not ideal practice
  await page.getByTestId("SignIn").click();
  
  await page.getByTitle("IoT Dashboard").click();
});
```


## 26. Child Elements
```jsx
test("locating child elements", async ({ page }) => {
  // for child element just use space
  await page.locator('nb-card nb-radio :text-is("Option 1")').click();
  // alternative chaining
  await page.locator('nb-card').locator('nb-radio').locator(':text-is("Option 2")')

  await page.locator('nb-card').getByRole('button', { name: 'Sign in'}).first().click();

  // suboptimal
  await page.locator('nb-card').nth(3).getByRole('button').click();
});
```

## 28. Parent elements
```jsx
test("locating parent elements", async ({ page }) => {
  await page
    .locator("nb-card", { hasText: "Using the Grid" })
    .getByRole("textbox", { name: "Email" })
    .click();
  await page
    .locator("nb-card", { has: page.locator("#inputEmail1") })
    .getByRole("textbox", { name: "Email" })
    .click();

  await page
    .locator("nb-card")
    .filter({ hasText: "Basic form" })
    .getByRole("textbox", { name: "Email" })
    .click();
  await page
    .locator("nb-card")
    .filter({ has: page.locator(".status-danger") })
    .getByRole("textbox", { name: "Password" })
    .click();

  await page
    .locator("nb-card")
    .filter({ has: page.locator("nb-checkbox") })
    .filter({ hasText: "Sign in" })
    .getByRole("textbox", { name: "Email" })
    .click();

  await page
    .locator(':text-is("Using the Grid")')
    .locator("..")
    .getByRole("textbox", { name: "Email" })
    .click();
});
```

## 27. Reusing the locators
```jsx
test("Reusing the locators", async ({ page }) => {
  const basicForm = page.locator("nb-card").filter({ hasText: "Basic form" });
  const emailField = basicForm.getByRole("textbox", { name: "Email" });

  await emailField.fill("test@test.com");
  await basicForm.getByRole("textbox", { name: "Password" }).fill("Welcome123");
  await basicForm.locator("nb-checkbox").click();
  await basicForm.getByRole("button").click();

  await expect(emailField).toHaveValue("test@test.com");
});

```

## 29. Extracting Values
```jsx
test("Extracting values", async ({ page }) => {
  // single text value
  const basicForm = page.locator("nb-card").filter({ hasText: "Basic form" });
  const buttonText = await basicForm.locator("button").textContent();
  expect(buttonText).toEqual("Submit");

  // all text values
  const allRadioButtonsLabels = await page
    .locator("nb-radio")
    .allTextContents();
  expect(allRadioButtonsLabels).toContain("Option 1");

  // input value
  const emailField = basicForm.getByRole("textbox", { name: "Email" });
  await emailField.fill("test@test.com");
  const emailValue = await emailField.inputValue();
  expect(emailValue).toEqual("test@test.com");

  const placeholderValue = await emailField.getAttribute('placeholder');
  expect(placeholderValue).toEqual('Email')
});
```
## 30. Assertions
```jsx
test("assertions", async ({ page }) => {
  const basicFormButton = page
    .locator("nb-card")
    .filter({ hasText: "Basic form" })
    .locator("button");

  // general assertions
  const text = await basicFormButton.textContent();
  expect(text).toEqual("Submit");

  // locator assertion - will wait for up to 5 seconds
  await expect(basicFormButton).toHaveText("Submit");

  // soft assertion - can continue even if the assertion has failed, not considered a good practice
  await expect.soft(basicFormButton).toHaveText("Submit5");
  await basicFormButton.click();
});
```


## 31. Auto Waiting
```jsx
import { expect, test } from "@playwright/test";

test.beforeEach(async ({ page }) => {
  await page.goto("http://www.uitestingplayground.com/ajax");
  await page.getByText("Button Triggering AJAX Request").click();
});

test("auto waiting", async ({ page }) => {
  const successButton = page.locator(".bg-success");

  // await successButton.click();

  // const text = await successButton.textContent();
  // expect(text).toEqual("Data loaded with AJAX get request.");

  await expect(successButton).toHaveText("Data loaded with AJAX get request.", {
    timeout: 20_000,
  });
});

test("alternative waits", async ({ page }) => {
  const successButton = page.locator(".bg-success");

  // wait for element
  // await page.waitForSelector(".bg-success");

  // wait for a particular response
  // await page.waitForResponse('http://www.uitestingplayground.com/ajax')

  // wait for network calls to be completed ('NOT RECOMMENDED')
  // await page.waitForLoadState('networkidle');

  const text = await successButton.allTextContents(); // this selector does not wait
  expect(text).toContain("Data loaded with AJAX get request.");
});
```

## 32. Timeouts
- **global timeout** - total duration of the entire test run (default: no timeout)
- **test timeout** - the time limit for a single test (default: 30s)
- **action timeout** - time limit for the action command (click(), fill()), (default: no timeout)
- **navigation tineout** - page.goto('/'), (default: no timeout);
- **expect timeout** - (default: 5s)
- can be configured in **playwright.config.ts** or in the tests directly

```jsx
test("timeouts", async ({ page }) => {
  // test.setTimeout(10_000);  // sets timeout for the test
  test.slow(); // increases the default timeouts by x3
  const successButton = page.locator(".bg-success");

  await successButton.click();
});
```


# V. UI Components
