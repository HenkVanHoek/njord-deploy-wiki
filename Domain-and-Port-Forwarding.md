# Domain & Port Forwarding 🌐

Since PiSelfhosting acts as an orchestrator for your self-hosted server, 
making your applications securely accessible from outside your home network 
requires a custom domain and router configurations.

---

## 1. Getting a Domain name

To access services like Nextcloud, you need a domain name (e.g., `home.com`). 
You have two main options:

*   **Free Subdomain**: Use services like [DuckDNS](https://www.duckdns.org/) 
    or [No-IP](https://www.noip.com/) to get a free subdomain.
*   **Paid Domain**: Purchase a custom domain from a registrar (e.g., 
    Cloudflare, Namecheap) to get full control over subdomains.

---

## 2. Setting up Dynamic DNS (DDNS)

Most home internet connections have a dynamic public IP address that changes 
periodically. 
You must set up a DDNS client (often supported directly inside your router or via 
software like AdGuard Home or NPM) to periodically update your domain record 
to point to your current home IP.

---

## 3. Router Port Forwarding

To route public traffic to your Raspberry Pi, you must configure port 
forwarding on your home router's NAT settings:

| Public Port | Protocol | Target IP | Private Port | Description |
| :--- | :--- | :--- | :--- | :--- |
| **80** | TCP | `<Raspberry_Pi_IP>` | **80** | HTTP challenge/routing |
| **443** | TCP | `<Raspberry_Pi_IP>` | **443** | Secure HTTPS traffic |

> ⚠️ **Security Warning**: Only open ports 80 and 443. Keep ports like 
> 22 (SSH) and 81 (NPM Admin Portal) closed to the public internet!