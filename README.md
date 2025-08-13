# Spotify Web Application Test Automation

[![Build Status](https://img.shields.io/badge/build-passing-brightgreen.svg)](https://github.com/your-username/spotify-automation)
[![Test Coverage](https://img.shields.io/badge/coverage-85%25-green.svg)](https://github.com/your-username/spotify-automation)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

## Overview

This repository contains a comprehensive test automation framework for the Spotify web application. The framework implements robust end-to-end testing scenarios including user authentication, playlist management, music playback, and core user workflows. Built using industry-standard tools and following the Page Object Model (POM) design pattern for enhanced maintainability and scalability.

## Features

- **Page Object Model (POM)** architecture for better code organization
- **Cross-browser compatibility** with support for Chrome, Firefox, and Edge
- **Parallel test execution** capabilities for faster test runs
- **Comprehensive reporting** with detailed test results and screenshots
- **Data-driven testing** support with external data sources
- **Continuous Integration** ready with CI/CD pipeline configuration

## Technology Stack

- **Test Framework**: TestNG
- **Automation Tool**: Selenium WebDriver
- **Build Tool**: Maven
- **Programming Language**: Java 11+
- **Reporting**: Allure Reports / ExtentReports
- **Version Control**: Git

## Prerequisites

Ensure the following software is installed on your system:

| Tool | Version | Download Link |
|------|---------|---------------|
| Java JDK | 11+ | [Oracle JDK](https://www.oracle.com/java/technologies/javase-downloads.html) |
| Maven | 3.6+ | [Apache Maven](https://maven.apache.org/download.cgi) |
| Git | Latest | [Git SCM](https://git-scm.com/downloads) |
| Chrome Browser | Latest | [Google Chrome](https://www.google.com/chrome/) |

## Installation & Setup

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/spotify-test-automation.git
cd spotify-test-automation
```

### 2. Install Dependencies
```bash
mvn clean install
```

### 3. Configuration Setup
Update the configuration files in `src/main/resources/`:

**WebConfigurations.properties**
```properties
# Browser Configuration
browser.type=CHROME
headless.mode=false
implicit.wait=10
explicit.wait=15

# Application URLs
base.url=https://open.spotify.com/
api.base.url=https://api.spotify.com/v1/

# Test Data
test.data.file=testdata/spotify-testdata.xlsx
```

**Reporting.properties**
```properties
# Reporting Configuration
report.path=test-output/reports/
screenshot.path=test-output/screenshots/
report.title=Spotify Test Automation Report
```

## Running Tests

### Execute All Tests
```bash
mvn clean test
```

### Execute Specific Test Suite
```bash
mvn clean test -Dsurefire.suiteXmlFiles=testng-suites/smoke-tests.xml
```

### Run Tests with Custom Browser
```bash
mvn clean test -Dbrowser=FIREFOX
```

### Run Tests in Headless Mode
```bash
mvn clean test -Dheadless=true
```

### Generate Test Reports
```bash
mvn allure:report
mvn allure:serve
```

## Project Architecture

```
spotify-test-automation/
│
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   ├── com/spotify/automation/
│   │   │   │   ├── browseractions/          # Browser management utilities
│   │   │   │   │   ├── BrowserFactory.java
│   │   │   │   │   └── BrowserManager.java
│   │   │   │   │
│   │   │   │   ├── driverfactory/           # WebDriver configuration
│   │   │   │   │   ├── DriverFactory.java
│   │   │   │   │   └── WebDriverManager.java
│   │   │   │   │
│   │   │   │   ├── elementactions/          # Web element interactions
│   │   │   │   │   ├── ElementActions.java
│   │   │   │   │   └── WaitActions.java
│   │   │   │   │
│   │   │   │   ├── listeners/               # TestNG listeners
│   │   │   │   │   ├── TestListener.java
│   │   │   │   │   └── ReportListener.java
│   │   │   │   │
│   │   │   │   ├── pages/                   # Page Object Model classes
│   │   │   │   │   ├── BasePage.java
│   │   │   │   │   ├── LoginPage.java
│   │   │   │   │   ├── HomePage.java
│   │   │   │   │   ├── PlaylistPage.java
│   │   │   │   │   └── ProfilePage.java
│   │   │   │   │
│   │   │   │   └── utilities/               # Utility classes
│   │   │   │       ├── ConfigReader.java
│   │   │   │       ├── DataProvider.java
│   │   │   │       ├── ScreenshotUtils.java
│   │   │   │       └── TestDataUtils.java
│   │   │   │
│   │   │   └── resources/
│   │   │       ├── config/
│   │   │       │   ├── WebConfigurations.properties
│   │   │       │   └── Reporting.properties
│   │   │       │
│   │   │       ├── testdata/
│   │   │       │   └── spotify-testdata.xlsx
│   │   │       │
│   │   │       └── drivers/                 # WebDriver binaries (if needed)
│   │   │
│   │   └── test/
│   │       └── java/
│   │           └── com/spotify/tests/
│   │               ├── BaseTest.java
│   │               ├── LoginTests.java
│   │               ├── SignUpTests.java
│   │               ├── PlaylistTests.java
│   │               ├── MusicPlayerTests.java
│   │               └── LogoutTests.java
│   │
├── testng-suites/
│   ├── smoke-tests.xml
│   ├── regression-tests.xml
│   └── full-suite.xml
│
├── test-output/                             # Generated test reports
├── .github/workflows/                       # CI/CD pipeline files
├── Dockerfile                               # Docker configuration
├── pom.xml                                  # Maven configuration
└── README.md
```

## Test Cases Coverage

### Authentication Module
- ✅ User Registration with valid credentials
- ✅ User Login with email/username
- ✅ Login with invalid credentials
- ✅ Password reset functionality
- ✅ User Logout

### Playlist Management
- ✅ Create new playlist
- ✅ Add songs to playlist
- ✅ Remove songs from playlist
- ✅ Delete playlist
- ✅ Share playlist

### Music Player
- ✅ Play/Pause functionality
- ✅ Skip to next/previous track
- ✅ Volume control
- ✅ Shuffle mode
- ✅ Repeat mode

### Search & Discovery
- ✅ Search for artists, albums, songs
- ✅ Filter search results
- ✅ Browse by genre
- ✅ Trending music section

## Continuous Integration

This project is configured for CI/CD with GitHub Actions. The pipeline includes:

- Automated test execution on push/pull requests
- Cross-browser testing
- Test report generation and publishing
- Slack/Email notifications for test results

### Pipeline Configuration
```yaml
# .github/workflows/test-automation.yml
name: Spotify Test Automation

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        browser: [chrome, firefox]
    
    steps:
    - uses: actions/checkout@v3
    - name: Set up JDK 11
      uses: actions/setup-java@v3
      with:
        java-version: '11'
        distribution: 'temurin'
    
    - name: Run tests
      run: mvn clean test -Dbrowser=${{ matrix.browser }}
    
    - name: Generate report
      run: mvn allure:report
      
    - name: Publish test results
      uses: dorny/test-reporter@v1
      if: success() || failure()
      with:
        name: Test Results (${{ matrix.browser }})
        path: target/surefire-reports/*.xml
        reporter: java-junit
```

## Docker Support

### Build Docker Image
```bash
docker build -t spotify-automation .
```

### Run Tests in Docker
```bash
docker run --rm -v $(pwd)/test-output:/app/test-output spotify-automation
```

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Code Quality Standards
- Follow Java coding conventions
- Maintain test coverage above 80%
- Add JavaDoc comments for public methods
- Write meaningful commit messages

## Troubleshooting

### Common Issues

**ChromeDriver compatibility issues**
```bash
# Update ChromeDriver automatically
mvn clean test -Dwebdriver.chrome.driver=auto
```

**Test failures due to timing issues**
```bash
# Increase wait times in configuration
implicit.wait=15
explicit.wait=20
```

**Memory issues during parallel execution**
```bash
# Adjust Maven memory settings
export MAVEN_OPTS="-Xmx2048m -XX:MaxPermSize=512m"
```



**Maintained by**: MOHAMED KAMAL
