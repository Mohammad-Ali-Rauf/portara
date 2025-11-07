# 🌐 Portara

**Secure, ephemeral API gateway for local development — share safely, without the cloud.**

Portara is a privacy-first tunneling utility that lets you expose your local web apps securely, with zero external dependencies.  
No ngrok. No vendor lock-in. No secrets leaking.

---

## ✨ Features
- 🔐 Self-hosted, encrypted tunnels (mutual TLS)
- ⏳ Ephemeral URLs that expire automatically
- ⚙️ Simple configuration and presets
- 🌍 Optional peer-to-peer mode for direct sharing
- 🧰 Lightweight dashboard built with TanStack Start

---

## ⚙️ Usage
```bash
# Start a secure tunnel to localhost:3000
portara expose 3000

# Generate a short-lived public link
https://portara.dev/ab12cd34 (expires in 15m)
````

---

## 🧠 Philosophy

Portara exists for developers who want **secure, self-reliant sharing** —
no third-party relay servers, no unnecessary complexity. Just clean, controlled exposure.

---

## 📜 License

MIT — free, open source, and self-hostable.
