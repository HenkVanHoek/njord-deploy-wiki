# NjordDeploy Wiki

This repository contains the documentation wiki for [NjordDeploy](https://github.com/HenkVanHoek/njord-deploy), a Flask-based application for provisioning and managing self-hosted services on single-board computers and Debian servers.

## Wiki Structure

The main pages of this wiki include:
* **[Home](Home.md):** High-level overview of NjordDeploy.
* **[Architecture and Mental Model](Architecture-and-Mental-Model.md):** Deep dive into the configuration structure and single source of truth.
* **[Developer Component Editor Guide](Developer-Component-Editor-Guide.md):** Instructions for developers creating and managing service metadata.
* **[Domain and Port Forwarding](Domain-and-Port-Forwarding.md):** Guide on routing traffic to your self-hosted instance.
* **[Reverse Proxy Guides](Reverse-Proxy-Guides.md):** Setting up secure access and SSL certificates using Caddy or Nginx Proxy Manager.

## Editing the Wiki Locally

To edit this wiki locally:
1. Clone the repository:
   ```bash
   git clone git@github.com:HenkVanHoek/njord-deploy-wiki.git
   ```
2. Modify or add Markdown files.
3. Commit and push your changes:
   ```bash
   git add .
   git commit -m "docs: update wiki page"
   git push origin master
   ```

*Note: GitHub Wiki pages are rendered directly from the Markdown files in this repository. The `Home.md` file acts as the default landing page on the GitHub Wiki UI.*
