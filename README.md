# Test-Automation-Framework

Maven-based Selenium automation framework using **Java + TestNG**. Implements Page Object Model (POM), parallel test execution, reusable utilities, and reporting. Designed to be extendable for CI/CD (Jenkins / GitHub Actions) with cross-browser support and future API automation.

---

## Table of Contents

* [What's included](#whats-included)
* [Prerequisites](#prerequisites)
* [Project structure](#project-structure)
* [Setup & run tests](#setup--run-tests)
* [Browser & environment configuration](#browser--environment-configuration)
* [Reporting](#reporting)
* [Parallel execution](#parallel-execution)
* [Extending the framework](#extending-the-framework)
* [CI/CD integration tips](#cicd-integration-tips)
* [Screenshots & test artifacts](#screenshots--test-artifacts)

---

## What's included

* Java + TestNG test automation skeleton
* Page Object Model (POM) pattern for UI tests
* Reusable helpers/utilities (waits, element actions, config loader)
* `pom.xml` for dependency & build management
* `resources/screenshots` placeholder for test screenshots
* Basic `.gitignore`

> NOTE: The repo currently contains the core skeleton. Add your tests under `src/test/java` and page objects under `src/main/java` (or the convention used in this project).

---

## Prerequisites

* Java JDK 8+ installed and `JAVA_HOME` set
* Maven 3.6+ installed (`mvn` available on PATH)
* A browser driver (e.g., chromedriver) or use WebDriverManager to auto-manage drivers
* IDE (IntelliJ / Eclipse) recommended

---

## Project structure (high level)

```
Test-Automation-Framework/
├─ .idea/                       # IDE config (optional)
├─ resources/
│  └─ screenshots/              # Test screenshots go here
├─ src/
│  ├─ main/java/                # Page Objects, utilities, config loaders
│  └─ test/java/                # TestNG test classes
├─ .gitignore
├─ pom.xml                      # Maven dependencies & build
└─ README.md
```

Adjust paths as necessary — this is a recommended organization.

---

## Setup & run tests

1. Clone the repository:

```bash
git clone https://github.com/onkarnargide/Test-Automation-Framework.git
cd Test-Automation-Framework
```

2. Build the project and download dependencies:

```bash
mvn clean compile
```

3. Run all tests:

```bash
mvn test
```

4. Run a specific TestNG suite (if `testng.xml` exists):

```bash
mvn -DsuiteXmlFile=testng.xml test
```

5. Run a single test class:

```bash
mvn -Dtest=MyTestClass test
```

---

## Browser & environment configuration

This framework expects browser and environment configuration to be externalized (properties / YAML / system properties).

Common options:

* Use `-Dbrowser=chrome` or `-Dbrowser=firefox` to switch browsers.
* Use `-Denv=qa` or environment-specific property files for base URLs and credentials.

Example:

```bash
mvn test -Dbrowser=chrome -Denv=staging
```

If WebDriverManager is included in `pom.xml`, drivers will be auto-managed. Otherwise, place driver binaries on PATH or specify paths in config.

---

## Reporting

* Integrate TestNG reports and any additional reporters (Allure / ExtentReports) by adding required dependencies and listeners in `pom.xml` and `testng.xml`.
* Store report outputs under a `target/reports` (or similar) directory and publish them from CI.

---

## Parallel execution

* TestNG supports parallel execution. Configure `testng.xml` or use Maven `surefire`/`failsafe` plugin settings.

Example `testng.xml` snippet:

```xml
<suite name="Suite" parallel="tests" thread-count="4">
  <test name="ChromeTests">...</test>
  <test name="FirefoxTests">...</test>
</suite>
```

Be sure your tests and page objects are thread-safe (avoid shared mutable state).

---

## Extending the framework

Suggestions to grow the framework:

* Add a `pageobjects` package and move page classes there.
* Add a `tests` package for TestNG tests grouped by feature or module.
* Add a `drivers` util to centralize WebDriver creation using the factory pattern.
* Add logging (SLF4J + Logback) and structured test logs.
* Add API automation modules (RestAssured) under `src/test/java/api` if required.
* Add data-driven support (CSV/Excel/JSON) and a `testdata` resource folder.

---

## CI/CD integration tips

* Add a `Jenkinsfile` or GitHub Actions workflow to run `mvn test` and publish reports.
* Use environment variables or secrets for credentials.
* Persist the `target` folder as a build artifact and publish test reports using the CI's report plugin.
* For cross-browser testing, integrate with cloud providers (BrowserStack, Sauce Labs) by adding remote WebDriver configuration.

---

## Screenshots & test artifacts

* Screenshots are saved under `resources/screenshots` by default (adjust as needed).
* Attach screenshots and logs to CI test results for failed tests.

---

## Contributing

1. Fork the repo
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit changes and push: `git push origin feature/your-feature`
4. Create a Pull Request describing your changes

Keep tests stable and avoid committing large driver binaries or personal IDE files.

---

## License & contact

This repository does not include a license file. Add a `LICENSE` (e.g., MIT) if you want to make it open-source-friendly.

For questions or help, please contact the repository owner at `https://github.com/onkarnargide`.

---

*README generated and tailored for the repository structure found in the project root. If you want, I can:*

* *Insert badges (build, coverage, license).*
* *Add a detailed example `testng.xml` and a sample test class.*
* *Add Allure / ExtentReports configuration and sample report screenshots.*

Tell me which of the above you want next, and I’ll add it to the README.\*
