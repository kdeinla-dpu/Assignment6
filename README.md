# SE333 – Assignment 6 (6%)  
### UI Testing with Playwright – Traditional vs LLM/MCP Approach

Repository
GitHub Link: [https://github.com/kdeinla-dpu/Assignment6](https://github.com/kdeinla-dpu/Assignment6)

I could not get MCP to work on my vscode, I tried using a node in intellij but I could not get it to compile. This is only
the playwrightTraditional implementation. I did get this one fully working though.

name: Playwright Traditional Test
on:
  push:
    branches: [ main, master ]
  pull_request:
    branches: [ main, master ]

jobs:
  test:
    runs-on: ubuntu-latest
    timeout-minutes: 60

      - name: Checkout Repository
        uses: actions/checkout@v5

      - name: Set up Java
        uses: actions/setup-java@v5
        with:
          distribution: 'temurin'
          java-version: '25'

      - name: Build Project
        run: mvn -B install -DskipTests --no-transfer-progress

      - name: Install Playwright Browsers
        run: mvn exec:java -e -Dexec.mainClass=com.microsoft.playwright.CLI -Dexec.args="install --with-deps"

      - name: Run Traditional Playwright Tests Only
        run: mvn test "-Dtest=playwrightTraditional.BookstoreTest"
