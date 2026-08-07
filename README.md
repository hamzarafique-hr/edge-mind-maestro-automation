# Edge Mind Maestro Automation

End-to-end mobile automation test suite built with [Maestro](https://maestro.mobile.dev/) for the **Edge Mind** Android application.

## Project Structure

```
├── .github/
│   └── workflows/
│       └── maestro_sanity.yaml        # CI/CD pipeline running on Genymotion Cloud
├── .maestro/
│   └── config.yaml                    # Global Maestro configuration
├── maestro_sanity/
│   ├── 01-onboarding/                 # Onboarding flow tests
│   ├── 01-tooltip/                    # Tooltip walkthrough tests
│   ├── 02-security-&-profile-settings/ # Settings & privacy tests
│   └── 03-file-viewers/               # File viewer tests
├── my-maestro-project/
│   ├── config.yaml                    # Project-specific Maestro config
│   ├── elements/                      # Page Object Model selectors
│   │   ├── login_page.js
│   │   └── onboarding_elements.js
│   └── tests/                         # Test flows
│       ├── 001-onboarding_flow.yaml
│       ├── 002_bypass_flow.yaml
│       └── login_flow.yaml
├── detailed-report.html               # Generated Maestro HTML report
└── pdf visual testing.yaml            # Visual testing configuration
```

## Applications Under Test

| App | Package ID | Description |
|-----|-----------|-------------|
<!-- | **Edge Mind** | `com.ondevice.ai.chat.assistant` | AI chat assistant focused on on-device privacy and local agent experiences |
| **PDF Reader** | `pdfreader.pdfviewer.officetool.pdfscanner` | PDF viewer and document tool with tooltip onboarding flows | -->

## Prerequisites

<!-- - [Maestro CLI](https://maestro.mobile.dev/) -->
- Android SDK / ADB
- Java 17 (for CI pipeline)
<!-- - Genymotion Cloud account (for device farm execution) -->

## Running Tests Locally

```bash
# Run all tests in a flow directory
maestro test maestro_sanity/01-tooltip/

# Run a specific test
maestro test my-maestro-project/tests/001-onboarding_flow.yaml

# Generate HTML report
maestro test --format html-detailed --output report.html <flow-path>
```

## CI/CD

Tests run automatically via GitHub Actions using Genymotion Cloud devices. The pipeline:
1. Downloads the APK from Google Drive
2. Spins up an Android 14 emulator on Genymotion Cloud
3. Installs the app and executes the Maestro test suite
4. Uploads the generated HTML report as an artifact

## Page Object Model

UI selectors are centralized in the `my-maestro-project/elements/` directory to promote reusability and reduce flakiness:

```yaml
- runScript: ../elements/onboarding_elements.js
- assertVisible: ${output.onboardingPage.welcomeTitle}
- tapOn: ${output.onboardingPage.nextButton}
```

## Test Coverage

- **Onboarding Flows**: Complete onboarding, skip/bypass, explicit category selection
- **Login Flows**: Sign-in assertions, agent download navigation
- **Tooltip Walkthroughs**: First-launch tooltips, skip behavior, returning user validation
- **Security & Privacy**: Conversation log purge, permanent erasure of local history
- **File Viewers**: PDF viewing and document handling

<!-- ## Notes

- `.github/` and `reports/` are gitignored locally but restored for CI
- Some flows use conditional execution (`runFlow` / `when`) for dynamic UI states
- The `detailed-report.html` file is generated after test execution and should not be committed to version control -->
