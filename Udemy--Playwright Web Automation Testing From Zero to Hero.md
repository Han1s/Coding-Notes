
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
- `npx playwright test --projeect=chromium` rns only for chromium
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
