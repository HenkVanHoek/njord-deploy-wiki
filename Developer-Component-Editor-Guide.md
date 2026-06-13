# Developer: Component Editor Guide 💻

The Component Editor is a powerful administrative workspace designed to create,
validate, and maintain components, user variables, and templates.

---

## 1. Creating a Component Skeleton

Click the **Create New Component** button in the sidebar. Enter a unique
Component ID (slug format: lowercase letters, numbers, and hyphens) and
a friendly display Name. 
The editor will automatically create the folder structures, a dummy compose template,
and an empty `variables.json` file.

---

## 2. Core Metadata Configuration

Within the **Core Metadata** tab, you configure:
*   **Group**: The category under which the component is shown in "Groups" view.
*   **Package ID**: Assigns the component to a preconfigured stack (like
    `nextcloud-stack`). If unassigned, leave empty to keep it as a Standalone item.
*   **Conflicts With**: List of other component IDs that cannot be installed
    alongside this component.

---

## 3. Designing Variables (`variables.json`)

Go to the **User Variables** tab. Here you define the form inputs shown to the
user during setup:
*   **Type**: Select `port` for port mappings, `path` for directories, or
    `password` for security inputs.
*   **Required**: Mark as required to force the user to input a value during
    installation.
*   **Special Macros**: Set the default value to `{{ CONFIG_BASE_PATH }}/path`
    for folder locations to guarantee absolute portability.

---

## 4. Writing Templates and Validation

In the **Template Editor** tab, write your standard `docker-compose.template.yml`
file. Wrap all configurable settings in Jinja tags (e.g., `{{ PORT_NEXTCLOUD }}`).

### Naming Conventions & Schema Verification:
Click **Validate Template** before saving. The backend validator will verify:
1.  That the YAML structure is valid.
2.  That any `container_name` declared inside the services strictly begins with the
    mandatory prefix `piselfhosting-` to prevent collisions on target machines.

---

## 5. Security Hash Generator

If you are setting up Basic Authentication, use our secure **Generate Hash** tool
at the top right. 
Enter a username and password to generate a secure, bcrypt-hashed string. 
Copy this string into your global `.env` file, and then safely reference it using
the macro `{{ DOTENV.YOUR_ENV_KEY }}`.

---

## 6. AI-Assisted Component Generation

The component editor includes an AI assistant that automatically bootstraps new components using a GitHub repository URL.

### Setup and Configuration
The generator communicates with the Gemini REST API using the model "gemini-2.5-flash".
To use this feature, you must provide a Gemini API Key:
- Option A: Define the key in the ".env" file in your root folder using the variable "GEMINI_API_KEY".
- Option B: Enter the key in the "Create with AI" dialog in the web interface. The key is saved locally in browser storage.

### How to Use
1. Start the Editor App.
2. Click the "Create with AI" button in the sidebar.
3. Input the GitHub repository URL (such as "https://github.com/caddyserver/caddy") and add optional custom instructions.
4. Click "Generate Component". The backend sends a request to the Gemini API with structural instructions and validation rules.
5. The API returns a structured JSON payload containing metadata, user variables, and a Docker Compose template.
6. Review the preview of the generated files.
7. Click "Accept and Create" to save the bootstrapped files directly to the local project filesystem.

---

## 7. Component Repository Synchronization

To decouple the release cycle of individual self-hosted services from the main application installer, components are stored and maintained in a separate repository.

- Remote Repository: "https://github.com/HenkVanHoek/piselfhosting-components"
- Custom Repository Variable: "PI_SELFHOSTING_COMPONENTS_REPO" (Defaults to "HenkVanHoek/piselfhosting-components")
- Branch Variable: "PI_SELFHOSTING_COMPONENTS_BRANCH" (Defaults to "main")

### How Synchronization Works
1. Fetching Remote Data:
   The application downloads the latest ZIP archive of the remote repository and extracts it to a local cache directory. On Linux, this is located inside the user data directory:
   "~/.local/share/PiSelfhosting/remote_components_cache"
2. Diff and Compare:
   The system compares local component templates and metadata against the cached remote version. It detects if components are synced, modified, only available locally, or only available remotely.
3. Synchronizing (Pull):
   The user can pull components individually or in bulk. Pulling overwrites the local templates and the local "components_metadata.json" with the remote version.
4. Publishing (Push):
   Developers with write access can push local components back to the remote repository. The sync manager verifies write permission by executing a dry-run push using SSH or HTTPS.
   To pass the validation gate during upload, the template file "docker-compose.template.yml" must start with the following header comments:
   - "# status: <status>"
   - "# last_tested_version: <version>"
   - "# platform_notes: <notes>"
   - "# breaking_changes: <changes>"

---

## 8. Local LLM and Context Generation (Ollama)

For offline development and deep codebase reasoning, you can run a local Mistral-based assistant.

### Setup and Configuration
1. Create a Model file:
   Create a file named "piselfhosting.mf" in the project root.
2. Build the Model in Ollama:
   Run the following terminal command:
   ```bash
   ollama create piselfhosting-expert -f piselfhosting.mf
   ```
3. Generate Codebase Context:
   Run the context generator script:
   ```bash
   python context_generator.py
   ```
   This script gathers all project code, runs a token count check to ensure it stays within the VRAM limit of an RTX 3060 (12GB VRAM), and produces the unified context file "llm_context.txt".
4. Ingest Context:
   Start a session with the "piselfhosting-expert" model in Open WebUI, then drag and drop the "llm_context.txt" file into your chat.