# Reverse Proxy Setup (NPM, Traefik, Caddy) 🛡️

A Reverse Proxy intercepts incoming web traffic on ports 80/443, 
terminates the SSL/TLS connection (using Let's Encrypt), and forwards 
the requests safely to the correct local container port.

---

## 1. Nginx Proxy Manager (NPM)

Nginx Proxy Manager is the easiest option for beginners due to its clean, 
web-based administration panel (accessible on port `81` on your Pi).

### Step-by-Step Proxy Host Creation:
1.  Log in to your NPM Admin panel on `http://<Raspberry_Pi_IP>:81`.
2.  Navigate to **Hosts** -> **Proxy Hosts** and click **Add Proxy Host**.
3.  Enter your subdomain (e.g., `nextcloud.yourdomain.com`).
4.  Set **Scheme** to `http`, **Forward IP** to your Raspberry Pi's local IP, 
    and **Forward Port** to the host port of the container (e.g., `8080`).
5.  Check **Websockets Support** (highly recommended for push services 
    and live sync).
6.  Go to the **SSL** tab, select **Request a new SSL Certificate**, 
    check **Force SSL**, and agree to the Terms of Service.
7.  Click **Save**. NPM will automatically issue a free SSL certificate!

---

## 2. Traefik Setup

Traefik is a modern, dynamic reverse proxy. If you checked the **Has Traefik 
Support** box in a component's metadata, NjordDeploy will automatically 
generate the correct router labels in the final compose file.

Traefik will read these labels directly and provision SSL certificates 
dynamically without any manual web interface configurations!

---

## 3. Caddy Setup

Caddy is a lightweight reverse proxy. If you prefer using Caddy, you can 
write a minimal `Caddyfile` on your host to route traffic securely:

```caddy
nextcloud.yourdomain.com {
    reverse_proxy localhost:8080
}

vault.yourdomain.com {
    reverse_proxy localhost:8081
}
```
Caddy will handle Let's Encrypt SSL certificates automatically on startup.