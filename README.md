# Playwright Automation

### Tools & Technologies
* Node JS
* VS Code
* JavaScript

### INSTALLING Playwright:

(Terminal)

Navigate to project folder and enter: `npm init playwright@latest`

(VS Code IDE)

Go to Extensions and search Playwright

Find Playwright by author Microsoft from list and choose ‘install’

Via Command Pallet menu (cmd + shift + P) search for Playwright 

Select dropdown option that says `Test: Install Playwright`

### RUNNING First Tests:

`npx playwright test` by default will run every test in the ‘tests’ directory of project files one by one in sequential order. 

To run particular test file:

`npx playwright test landing-page.spec.ts`

Other Flags:

`--ui` Starts the interactive UI mode

`--project` to specify browser, i.e.: 

`npx playwright test --project webkit` 

`npx playwright test --project firefox`

And multiple brosers:

`npx playwright test --project webkit --project firefox`

Run last failed test: `npx playwright test --last-failed`

`--debug` Starts the test in debug mode (opening Playwright inspector window)

`--workers 3` Starts the test in parallel using three workers 

### READING Reports:

`npx playwright show-report` will open html report file

You can also access report file by navigating to the `playwright-report` directory within project hierarchy.

### WRITING First Test:

Create filename in tests directory

Include playwright test module in the script: `import { test, expect } from '@playwright/test';`

Or: `const {test, expect} = require(‘@playwright/test’)`

Syntax:
```
test(‘name of test’, async ({ page }) => {
    await page.goto(‘https://playwright.dev/')
    await expect(page.toHaveTitle(/Playwright/)
```

### GENERATING Tests:

`npx playwright codegen`

or `npx playwright codegen --browser firefox`

Manually navigate and click through actions. Note output in Playwright inspector. 

Record and save to file: `npx playwright codegen --target javascript -o record_example.js`

Set viewport: `npx playwright codegen --viewport-size=800,600`

Emulate device: `npx playwright codegen --device="iPhone 15"`

Emulate color scheme: `npx playwright codegen --color-scheme=dark playwright.dev`

Emulate geolocation, language and timezone: 

`npx playwright codegen --timezone="Europe/Rome" --geolocation="41.890221,12.492348" --lang="it-IT" bing.com/maps`

### TRACE Viewer:

playwright.config.js:
`trace: 'on-first-retry',` (default setting) Allows you to inspect DOM snapshots to review details of test runs, including error messages of failed tests. 

`await page.pause()` for debugging in Playwright inspector

### LOCATORS:

Using any object property:

`await page.locator('id=user-name')`

or: `await page.locator('[id="user-name"]').fill('Einstein')

Using CSS:

#login-button, for exmaple:

`await page.locator('#login-button').click()`

Playwright inspector can be used here (page.pause()) and 'Explore' in the Playwright inspector.

### ASSERTIONS

Uses expect functions. Call expect(value) and choose matcher that reflects expectation. 

Different types of assertions:

Generic matchers (toEqual, toContain, toBeTruthy)

auto-retrying

non-retying

negative matchers, e.g.: `expect(value).not.toEqual(0)` for example

soft assertions: `await expect.soft(page.getByTestId('status')).toHaveText('Success))` -- does not stop test if fails

custom expect message: `await expect(page.getByText('Name'), 'should be logged in').toBeVisible();` --shows up in reporting

### RECORDING Tests

playwright.config.js:
```
  use: {
    video: 'on-first-retry',
```

### HOOKS

beforeAll/afterAll

Declares a beforeAll/afterAll hook that is executed once per worker before or after all tests.

When called in the scope of a test file, runs before/after all tests in the file. When called inside a test.describe() group, runs before/after all tests in the group.

beforeEach/afterEach

Same as above, but with different frequency according to number of tests in spec file.

describe (groups of tests)

Allows you to group series of tests in the same file.

### ANNOTATIONS

test.skip()

test.fail()

test.fixme()

test.slow()

test.only()

test.skip()

### PAGE Object Models

Creates helper class to encapsulate common selectors in one place for ease of repeated use.

Example - login spec:
```
import { test, expect } from '@playwright/test';
import { LoginPage } from '../../pages/login'

test('test', async ({ page }) => {

  const Login = new LoginPage(page)

  await Login.gotoLoginPage()
  await Login.login('tomsmith', 'SuperSecretPassword!')
});
```
Uses page objects in login.js:

```
exports.LoginPage = class LoginPage {

    constructor(page) {

        this.page = page
        this.username_textbox = page.getByLabel('Username')
        this.password_textbox = page.getByLabel('Password')
        this.login_button = page.getByRole('button', { name: 'Login' })
    }

    async gotoLoginPage(){
        await this.page.goto('https://the-internet.herokuapp.com/login');
    }

    async login(username, password){
        await this.username_textbox.fill(username)
        await this.password_textbox.fill(password)
        await this.login_button.click()
    }
}
```
### API Testing

GET 
```
import { test, expect } from '@playwright/test';

test('API GET Request ', async ({request}) => {
    const response = await request.get('https://reqres.in/api/users/2')
    expect(response.status()).toBe(200);
    const text = await response.text();
    expect(text).toContain('Janet')
    console.log(await response.json());
})
```
POST:
```
test('API POST', async ({ request }) => {
    const response = await request.post('https://reqres.in/api/users', {
        data: {
            "name": "morpheus",
            "job": "leader"
        }
    })
    expect(response.status()).toBe(201);
    const text = await response.text();
    expect(text).toContain('morpheus');
    console.log(await response.json());
})
```
PUT

DELETE

Validate API Response, Checking response, logs, errors in UI mode.

