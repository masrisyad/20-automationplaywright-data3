```markdown
# Kelasku Info Edit Automated Test

This project is an automated testing script built with Python and [Playwright](https://playwright.dev/python/). It simulates a user logging into a web application, navigating to the "Kelasku" section, editing information within a rich text editor, and capturing the final state. 

After the test concludes, the script generates a comprehensive PDF report containing test logs, a success rate chart, and visual evidence (screenshot). If configured, it will automatically email this report to designated recipients using the Mailjet API.

## Features

* **Automated UI Testing:** Uses asynchronous Playwright for fast and reliable browser automation.
* **Smart Locators:** Implements multiple fallback selectors for interacting with dynamic UI elements (like edit buttons and iframes) to ensure test stability.
* **Rich PDF Reporting:** Uses `fpdf` and `matplotlib` to generate a customized PDF report featuring:
  * A Pass/Fail success rate donut chart.
  * A detailed table of step-by-step test logs.
  * Attached screenshot evidence.
* **Email Notifications:** Seamlessly attaches and sends the generated PDF report via Mailjet.

## Prerequisites

Before running the script, ensure you have the following installed on your machine:

* **Python 3.8+**
* **pip** (Python package installer)

## Installation

1. **Clone or download the project folder.** Ensure your script and the accompanying `settings.py` file are in the same directory.
2. **Install the required Python dependencies:**
   ```bash
   pip install playwright fpdf matplotlib mailjet_rest

```

3. **Install the required Playwright browser binaries:**
```bash
playwright install chromium

```



## Configuration

The script is highly customizable through Environment Variables. You can set these in a `.env` file or export them directly in your terminal.

### Test Environment Variables

* `KELASKU_EDIT_INFO_TEXT`: The text to input into the editor (Default: `Test Edit [Timestamp]`).
* `TIMEOUT_MS`: Maximum wait time for UI elements to load, in milliseconds (Default: `10000`).
* `WAIT_AFTER_ACTION_SECONDS`: How long to wait after submitting the edit before taking a screenshot (Default: `3`).
* `SCREENSHOT_PATH`: Filename/path for the captured evidence (Default: `screenshot3_kelasku_info_edit.png`).
* `REPORT_PATH`: Filename/path for the final PDF report (Default: `test_report_kelasku_info_edit.pdf`).

### Required Configuration in `settings.py`

Because this script imports `EmailConfig` and `LoginConfig` from a local `settings.py` file, ensure those classes are properly loading the following data (typically also via environment variables):

* **Application Credentials:** Web app Login URL, Username, and Password.
* **Mailjet Credentials:** `SEND_EMAIL` (must be `true`), `MAILJET_API_KEY`, and `MAILJET_API_SECRET`.
* **Email Routing:** Sender/Recipient email addresses, names, subject, and body text.

## Usage

To execute the automated test, simply run the script from your terminal:

```bash
python main.py

```

*(Replace `main.py` with the actual filename of your script).*

## Expected Output

Upon execution, the terminal will print real-time execution logs. Once finished, you will find two new files in your directory:

1. **Screenshot file** (e.g., `screenshot3_kelasku_info_edit.png`) showing the webpage right after the edit is submitted.
2. **PDF Report file** (e.g., `test_report_kelasku_info_edit.pdf`) containing the summary, charts, and evidence.

If `SEND_EMAIL=true` is properly configured, you will also see a console message confirming the email delivery status.
