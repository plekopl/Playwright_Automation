Playwright Automation


TWO ways of installing: 

1. IN TERMINAL: 

Navigate to project folder and enter: `npm init playwright@latest`

2. VS CODE EXTENSION: 

Go to Extensions and search Playwright
Find Playwright by author Microsoft from list and choose ‘install’
Via Command Pallet menu (cmd + shift + P) search for Playwright 
Select dropdown option that says `Test: Install Playwright`

RUNNING First Tests:

`npx playwright test` by default will run every test in the ‘tests’ directory of project files one by one in sequential order. 
To run particular test file, include its filename at the end of the command

Flags for test command:

`--ui` Starts the interactive UI mode
`--project=chromium` Runs the tests only on Desktop Chrome (or other browser as specified)
`--debug` Starts the test in debug mode (opening Playwright inspector window)
`--workers 3` Starts the test in parallel using three workers 

Reading Reports

`npx playwright show-report` will open html report file

You can also access report file by navigating to the `playwright-report` directory within project hierarchy.

WRITING First Test

Create filename in tests directory
Include playwright test module in the script: `import { test, expect } from '@playwright/test';`
Or: `const {test, expect} = require(‘@playwright/test’)`

Syntax:

`test(‘name of test’, async ({ page }) => {
	await page.goto(‘https://plarwright.dev/')
	await expect(page.toHaveTitle(/Playwright/)`


RECORD Test

`npx playwright codegen`