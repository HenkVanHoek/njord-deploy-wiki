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