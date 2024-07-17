# Playwright_Automation

Notes on setup

2 ways to install: 

1. IN TERMINAL: 

Navigate to project folder and enter: `npm init playwright@latest`

2. IN VS CODE: 

Go to Extensions and search `Playwright`
Find Playwright by author Microsoft from list and choose `install`
From Command Pallet menu (cmd + shift + P) search for Playwright 
Select dropdown option that says `Test: Install Playwright `

Running First Tests

`npx playwright test` by default will run every test in the ‘tests’ directory of project files one by one in sequential order. 
Including a filename at the end of the command will limit the run to that specific test.

Flags for test command:

`--ui` Starts the interactive UI mode
`--project=chromium` Runs the tests only on Desktop Chrome
`--debug` Starts the test in debug mode

Reading Reports

`npx playwright show-report` launches HTML based report in browser via localhost:9323
