# Install UAEJobs on macOS

This guide is written for first-time users. You do not need to know how to code.

UAEJobs has two parts:

- **Chrome extension:** shows the analyzer on LinkedIn.
- **UAEJobs CLI:** saves jobs locally, provides your matching profile, connects Gmail, and keeps the extension connected.

Your job data stays on your Mac. UAEJobs does not automatically apply for jobs.

## Before you begin

You need a Mac with Google Chrome, Python 3.9 or newer, and these files from the [UAEJobs 0.18.1 release](https://github.com/mattldsouza/uaejobs/releases/tag/v0.18.1):

- `uaejobs-extension-1.0.38.zip`
- `uaejobs_cli-0.18.1-py3-none-any.whl`

To check Python, open Terminal and run `python3 --version`. The `.whl` file is a Python installer—do not double-click it. macOS will say that no application can open it.

## Part 1 — Install the Chrome extension

### Unzip and keep the extension

1. Open **Finder → Downloads**.
2. Double-click `uaejobs-extension-1.0.38.zip`.
3. Move the resulting folder to a permanent location such as **Documents/UAEJobs Extension**.
4. Do not delete or move that folder after loading it into Chrome.

### Load it into Chrome

1. Open Chrome.
2. Enter `chrome://extensions` in the address bar and press Return.
3. Turn on **Developer mode** in the upper-right corner.
4. Click **Load unpacked**.
5. Select the unzipped folder containing `manifest.json`.
6. Open Chrome's puzzle-piece menu and pin **UAEJobs LinkedIn Analyzer**.

Open a LinkedIn job and click the UAEJobs icon. The analyzer should appear. It may show **CLI OFFLINE** until Part 2 is complete.

## Part 2 — Install the local UAEJobs service

### What is Terminal?

Terminal is a built-in macOS app for entering commands. Press **Command + Space**, type **Terminal**, and press Return. Copy and run each command below separately, waiting for it to finish before continuing.

### Go to Downloads

```bash
cd ~/Downloads
```

### Install UAEJobs

```bash
python3 -m pip install --user "uaejobs_cli-0.18.1-py3-none-any.whl[gmail]"
```

If macOS reports an `externally-managed-environment` error, use `pipx`:

```bash
brew install pipx
pipx ensurepath
pipx install "uaejobs_cli-0.18.1-py3-none-any.whl[gmail]"
```

Close and reopen Terminal after `pipx ensurepath` if it cannot find `uaejobs`.

### Confirm the installation

```bash
uaejobs --version
```

Expected result:

```text
uaejobs 0.18.1
```

### Start the private connector

```bash
uaejobs connector enable
uaejobs connector status
```

The connector runs only on your Mac at `127.0.0.1:8765`; it is not a public server. Return to LinkedIn and reload the page. The extension should now show **CLI CONNECTED**.

## Part 3 — Gmail sync (optional)

The LinkedIn analyzer works without Gmail sync. Gmail sync imports LinkedIn job-alert emails automatically and requests read-only access—it cannot send, edit, or delete email.

1. In Google Cloud, create a **Desktop app** OAuth client for the Gmail API.
2. Download its client JSON file.
3. In Terminal, type `uaejobs gmail connect ` with a space at the end.
4. Drag the downloaded JSON file from Finder into Terminal. Its full path appears automatically.
5. Press Return and approve the read-only permission in the browser.
6. Run:

```bash
uaejobs gmail status
uaejobs sync
uaejobs autosync enable
uaejobs autosync status
```

After connecting, move the downloaded client JSON to Trash. Never upload that file or `gmail-token.json` to GitHub or share them.

## Test the installation

1. Open a LinkedIn job.
2. Click the pinned UAEJobs icon.
3. Confirm the title, company, and location appear.
4. Confirm it says **CLI CONNECTED**.
5. Click **Send to UAEJobs**.
6. Run `uaejobs extension-imports` in Terminal and confirm the job appears.

## Common problems

### Chrome says the manifest is missing

Select the inner extension folder containing `manifest.json`.

### `command not found: uaejobs`

Close and reopen Terminal. If you used `pipx`, run `pipx ensurepath` and reopen Terminal again.

### The extension says CLI OFFLINE

```bash
uaejobs connector status
uaejobs connector enable
```

Then reload LinkedIn.

### Gmail authorization expired or was revoked

Download a new Desktop OAuth client JSON and run `uaejobs gmail connect` again using the drag-and-drop method above.

### The extension does not appear

Open `chrome://extensions`, confirm UAEJobs is enabled, and click **Reload**. If needed, use **Load unpacked** again and select the permanent extension folder.

## Updating later

Install a newer CLI wheel with `--upgrade`. Replace the files in the permanent extension folder with the new ZIP contents, then click **Reload** on the extension card in `chrome://extensions`.

Your database, candidate profile, Gmail token, and panel position are stored outside the release package and should remain intact.
