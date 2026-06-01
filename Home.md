```markdown
# Welcome to the PiSelfhosting Wiki 🚀

PiSelfhosting is a modular, lightweight, and sovereign stack orchestrator 
designed to deploy self-hosted services onto Debian and Raspberry Pi servers. 
It completely eliminates the manual hassle of writing docker-compose files, 
managing networks, and configuring reverse proxies.

---

## 💡 The Mental Model

To understand how PiSelfhosting organizes your home server, we use three 
core concepts:

```
+-----------------------------------------------------------------+
|                           Groups                                |
|  - Categories (e.g. databases, network, productivity)           |
|  - Used for organizing independent standalone components         |
+-----------------------------------------------------------------+
                                |
                                v
+-----------------------------------------------------------------+
|                          Components                             |
|  - The atomic unit: a single container definition               |
|  - Contains metadata, user variables, and compose templates     |
+-----------------------------------------------------------------+
                                |
                                v
+-----------------------------------------------------------------+
|                          Packages                               |
|  - Preconfigured stacks of coupled components                   |
|  - Example: Nextcloud App + MariaDB + Redis + Notify Push       |
+-----------------------------------------------------------------+
```

1. **Components**: The atomic building blocks (e.g., `nextcloud-app`, 
   `nextcloud-db`, `vaultwarden`). Each component has its own template, 
   configurations, and isolated metadata.
2. **Groups (Categories)**: Logical groupings (e.g., `Databases`, 
   `Productivity`, `Network`) used in the standard setup to browse and 
   select standalone components.
3. **Packages (Stacks)**: Bound compositions of components designed to 
   work together as a single preconfigured stack (e.g., the `nextcloud-stack` 
   combining the portal, database, redis cache, and push dumper).

---

## 📚 Wiki Table of Contents

Navigate through the documentation using the guides below:

### 🛠️ Getting Started & Networking
*   **[Domain & Port Forwarding](Domain-and-Port-Forwarding)**  
    Learn how to configure your router, manage DNS records, and forward 
    port 80 and 443 to your Raspberry Pi.
*   **[Reverse Proxy Setup (NPM, Traefik, Caddy)](Reverse-Proxy-Guides)**  
    Choose and configure your reverse proxy of choice to automatically 
    generate SSL certificates and route secure traffic to your services.

### 🧠 Architecture & Deep Dive
*   **[Architecture & Design Patterns](Architecture-and-Mental-Model)**  
    A technical deep dive into our modular component design, variable 
    macro injection system, and the backend CQRS pattern.

### 💻 Developer Guides
*   **[Developer Component Editor Guide](Developer-Component-Editor-Guide)**  
    A step-by-step guide to creating, updating, and validating components, 
    managing variables, and generating secure authorization hashes within 
    the Developer Editor.
```