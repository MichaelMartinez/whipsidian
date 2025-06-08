# Obsidian Sample Plugin

This is a sample plugin for Obsidian (<https://obsidian.md>).

This project uses TypeScript to provide type checking and documentation.
The repo depends on the latest plugin API (obsidian.d.ts) in TypeScript Definition format, which contains TSDoc comments describing what it does.

This sample plugin demonstrates some of the basic functionality the plugin API can do.

- Adds a ribbon icon, which shows a Notice when clicked.
- Adds a command "Open Sample Modal" which opens a Modal.
- Adds a plugin setting tab to the settings page.
- Registers a global click event and output 'click' to the console.
- Registers a global interval which logs 'setInterval' to the console.

## First time developing plugins?

Quick starting guide for new plugin devs:

- Check if [someone already developed a plugin for what you want](https://obsidian.md/plugins)! There might be an existing plugin similar enough that you can partner up with.
- Make a copy of this repo as a template with the "Use this template" button (login to GitHub if you don't see it).
- Clone your repo to a local development folder. For convenience, you can place this folder in your `.obsidian/plugins/your-plugin-name` folder.
- Install NodeJS, then run `npm i` in the command line under your repo folder.
- Run `npm run dev` to compile your plugin from `main.ts` to `main.js`.
- Make changes to `main.ts` (or create new `.ts` files). Those changes should be automatically compiled into `main.js`.
- Reload Obsidian to load the new version of your plugin.
- Enable plugin in settings window.
- For updates to the Obsidian API run `npm update` in the command line under your repo folder.

## Releasing new releases

- Update your `manifest.json` with your new version number, such as `1.0.1`, and the minimum Obsidian version required for your latest release.
- Update your `versions.json` file with `"new-plugin-version": "minimum-obsidian-version"` so older versions of Obsidian can download an older version of your plugin that's compatible.
- Create new GitHub release using your new version number as the "Tag version". Use the exact version number, don't include a prefix `v`. See here for an example: <https://github.com/obsidianmd/obsidian-sample-plugin/releases>
- Upload the files `manifest.json`, `main.js`, `styles.css` as binary attachments. Note: The manifest.json file must be in two places, first the root path of your repository and also in the release.
- Publish the release.

> You can simplify the version bump process by running `npm version patch`, `npm version minor` or `npm version major` after updating `minAppVersion` manually in `manifest.json`.
> The command will bump version in `manifest.json` and `package.json`, and add the entry for the new version to `versions.json`

## Adding your plugin to the community plugin list

- Check the [plugin guidelines](https://docs.obsidian.md/Plugins/Releasing/Plugin+guidelines).
- Publish an initial version.
- Make sure you have a `README.md` file in the root of your repo.
- Make a pull request at <https://github.com/obsidianmd/obsidian-releases> to add your plugin.

## How to Install and Run the Plugin

To get this plugin running in your Obsidian vault, follow these steps:

### 1. Setup the Obsidian Plugin (Frontend)

1. **Clone the Repository:**

    ```bash
    git clone https://github.com/your-username/obsidian-whisper-llm-plugin.git
    cd obsidian-whisper-llm-plugin
    ```

    (Replace `https://github.com/your-username/obsidian-whisper-llm-plugin.git` with the actual repository URL)

2. **Install Node.js Dependencies:**
    Make sure you have Node.js (v16 or later recommended) installed.

    ```bash
    npm install
    ```

3. **Compile the Plugin:**
    Run the development script to compile the TypeScript code into JavaScript. This will also watch for changes.

    ```bash
    npm run dev
    ```

    This will generate `main.js`, `styles.css`, and `manifest.json` in the root of the project.

4. **Manually Install in Obsidian:**
    Copy the generated `main.js`, `styles.css`, and `manifest.json` files into your Obsidian vault's plugin folder.
    - Navigate to your Obsidian vault (e.g., `MyVault/.obsidian/plugins/`).
    - Create a new folder named `obsidian-whisper-llm-plugin` (or a similar descriptive name).
    - Paste `main.js`, `styles.css`, and `manifest.json` into this new folder.
    - Your path should look something like: `MyVault/.obsidian/plugins/obsidian-whisper-llm-plugin/main.js`

5. **Enable the Plugin in Obsidian:**
    - Open Obsidian.
    - Go to `Settings` (gear icon on the bottom left).
    - Navigate to `Community plugins`.
    - Turn off `Restricted mode` if it's on.
    - Under `Installed plugins`, toggle on `Obsidian Whisper + LLM Agent Plugin` (or whatever the plugin name is in `manifest.json`).

### 2. Setup the Python Backend

1. **Navigate to the Python Backend Directory:**

    ```bash
    cd python-backend
    ```

2. **Create and Activate a Virtual Environment (Recommended):**

    ```bash
    python -m venv venv
    # On Windows:
    .\venv\Scripts\activate
    # On macOS/Linux:
    source venv/bin/activate
    ```

3. **Install Python Dependencies:**

    ```bash
    pip install -r requirements.txt
    ```

4. **Run the FastAPI Server:**

    ```bash
    uvicorn main:app --reload
    ```

    This will start the backend server, typically accessible at `http://127.0.0.1:8000`. Keep this terminal window open as long as you are using the plugin.

### 3. Test Communication (Ping-Pong)

1. **In Obsidian:**
    - Open the Command Palette (`Ctrl+P` or `Cmd+P`).
    - Search for "Ping Python Backend" and select it.
    - You should see a notice pop up in Obsidian saying "Python Backend Response: pong", confirming successful communication.

## Improve code quality with eslint (optional)

- [ESLint](https://eslint.org/) is a tool that analyzes your code to quickly find problems. You can run ESLint against your plugin to find common bugs and ways to improve your code.
- To use eslint with this project, make sure to install eslint from terminal:
  - `npm install -g eslint`
- To use eslint to analyze this project use this command:
  - `eslint main.ts`
  - eslint will then create a report with suggestions for code improvement by file and line number.
- If your source code is in a folder, such as `src`, you can use eslint with this command to analyze all files in that folder:
  - `eslint .\src\`

## Funding URL

You can include funding URLs where people who use your plugin can financially support it.

The simple way is to set the `fundingUrl` field to your link in your `manifest.json` file:

```json
{
    "fundingUrl": "https://buymeacoffee.com"
}
```

If you have multiple URLs, you can also do:

```json
{
    "fundingUrl": {
        "Buy Me a Coffee": "https://buymeacoffee.com",
        "GitHub Sponsor": "https://github.com/sponsors",
        "Patreon": "https://www.patreon.com/"
    }
}
```

## API Documentation

See <https://github.com/obsidianmd/obsidian-api>
