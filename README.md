# 🌐 Portara

## Status: In Development  
**TL;DR:** Localhost → temporary URL → share. Done.  
**📦 Requires:** [Bun](https://bun.sh) & TypeScript  

> ⚠️ Linux/macOS only for now.  
> 🪟 No Windows support planned (I don’t use it).  
> 💡 PRs welcome—but Portara’s soul is **open-source**, and Windows just isn’t part of that world.

<details>
<summary>💬 Why Bun only?</summary>
> The whole stack runs on Bun – CLI, coordinator, dashboard. No Bun, no magic.  
> “One runtime = one mental model.”
</details>

---

```
🔒 All tunnels are end-to-end encrypted.  
   Why trust me?  
     1️⃣ I’m too broke to afford a server that could log your data (I’d rather buy a GPU for local LLMs).  
     2️⃣ Zero interest in your data—I’ve got plenty of my own chaos already.  
     3️⃣ The source is public. Go ahead, peek.
```

*(“Wait, where's the setup?” There isn’t any. That’s the magic.)*

---

## 🚨 The Problem

Trying to show your local work **shouldn’t** require:
- Creating yet another SaaS account  
- Reading 47 pages of docs  
- Debugging `docker-compose.yml` until 3 AM  
- Becoming an HTTP/2 expert *(we have lives, people)*

You just wanna share. Not become a DevOps engineer.  
*(I’ve suffered so you don’t have to.)*

---

## 💡 The Solution

> ⏱️ URLs are **ephemeral** — 15 minutes by default. Adjust in `portara.toml` if needed.

```bash
curl -fsSL https://install.portara.netlify.app | sh -
portara expose 3000
```

**Boom.** You get a URL. Share it. It works. It vanishes later.

<details>
<summary>🤔 Netlify? Is this a cloud thing?</summary>
> Chill — Netlify only hosts the install script. **Everything else runs locally.**
</details>

---

## 🔐 For the Paranoid (Like Me)

**Option A (Normal):**  
```bash
curl -fsSL https://install.portara.netlify.app | sh -
```

**Option B (Read First):**  
```bash
git clone https://github.com/Mohammad-Ali-Rauf/portara
cat portara/install.sh
cd portara && bun ./install.sh
```

**Option C (DIY):**  
```bash
# Compile from source (you’re on your own)
```

> **Bottom line:** Code is public. Script is 100 lines. Coordinator runs **locally**.  
> Still nervous? Maybe don’t run random tunneling tools.

---

<details>
<summary>⚡ Technical Deep Dive</summary>

### How It Works

When you run `portara expose`, here’s the flow:

```
[Your App]  
    │
    ▼
[Portara CLI] ←→ [Local Coordinator] ←→ [Encrypted Tunnel] ←→ [Public URL]
    ▲
    │
[You (via terminal or dashboard)]
```

✅ **All components run on your machine**  
✅ **Tunnels are end-to-end encrypted**  
✅ **No data leaves your box unless you’re actively sharing**

The coordinator is a lightweight Elysia.js server that handles routing, encryption, and tunnel lifecycle—locally, always.

</details>

<details>
<summary>🧩 What’s the “Local Coordinator”?</summary>

A tiny backend that runs **on your machine**, acting as the hub for all Portara operations.

**Tech Stack:**  
- CLI → TypeScript + Bun.js  
- Coordinator → Elysia.js  
- Dashboard → TanStack Start  

Clean. Simple. No overengineering.
</details>

---

## 🚀 Commands

```bash
# The classics:
portara expose <port>    # Create tunnel  
portara close <port>     # Kill tunnel  
portara list             # List active tunnels  

# The extras:
portara config           # Tweak settings (optional)

# The “I’m fancy” tier:
portara freeze <port>    # ❄️ Pause tunnel (URL preserved, traffic stops)  
portara unfreeze <port>  # ▶️ Resume tunnel
```

<details>
<summary>❄️ Freeze/Unfreeze Explained</summary>

Freezing a tunnel **Freezing pauses traffic and stops the expiration timer, so your tunnel picks up right where it left off.**.  
Example:  
- You start a tunnel (15-min TTL)  
- Run for 2 minutes → **13 mins left**  
- Freeze for 1 hour → timer **doesn’t tick**  
- Unfreeze → still **13 minutes remaining**

Perfect for demos, meetings, or coffee breaks without losing your URL.
</details>

<details>
<summary>🛠️ Programmable & Configurable</summary>

- Config via `portara.toml` (optional)  
- Automate tunnels, script workflows, customize TTL  
- *“But I just want to share localhost?”* → Cool, ignore all this.
</details>

<details>
<summary>🏗️ Advanced Mode: Real-World Use Cases</summary>

While the install script handles everything for most users, you *can* run the coordinator manually:

```bash
docker run -p 8080:8080 mohammadalirauf/portara/coordinator
```

**Why would you?**  
- **CI/CD pipelines**: Pre-spin a coordinator in a test container to validate tunnel behavior  
- **Containerized demos**: Bundle your app + Portara coordinator in a single Docker Compose setup for live workshops  
- **Air-gapped dev**: Audit & run coordinator in isolated environments
- **Making your own client**: Create your own client which hits the coordinator's API

> ⚠️ But honestly—if you’re not doing something like this, just use the one-liner. Less work = more coffee ☕.
</details>

---

## ✅ Why This Doesn’t Suck

| Feature                | Traditional Tools 🥱          | **Portara** 🚀               |
|------------------------|-------------------------------|------------------------------|
| **Signup Required?**   | ✉️ Email? Phone? Soul?        | ❌ **No signup** — not even spammy emails |
| **Credit Card?**       | 💳 “Free tier” with strings   | ❌ **No credit card** — SaaS overlords blocked |
| **Config Files?**      | 📄 `ngrok.yml`, `.env`, `nginx.conf`… | ❌ No config — unless you’re bored and **want** to geek out. |
| **Cloud Dependency?**  | ☁️ Your data routes through their servers | 💻 **Everything local** — your machine, your rules |
| **Speed**              | ⏳ “Hold on while I read the docs…” | ⚡ **Works in <10 sec** — or your localhost owes you an apology |

---

## 🎯 Reasons I built it?

Portara = **“I don’t have time for this shit”** localhost sharing. Perfect when:
- Your designer needs to see the UI **NOW**  
- Your client’s refreshing their email like it’s a slot machine  
- You hate pay-as-you-go pricing with surprise bills  
- You just want it to **work**, not become a networking PhD  

> *“But what about enterprise features?”*  
> Bro. You got a secure, temporary URL in **under 10 seconds**.  
> Sometimes that’s **plenty**.

---

<details>
<summary>🛠️ Want to help me?</summary>
   
Clone the repo, run `bun install`, and check `DEVELOP.md` *(when it exists… probably after coffee ☕)*.
</details>

## 📜 License

MIT — free, open source, and **gloriously hackable**.

---

Try it or don’t.  
Your localhost-sharing anxiety? That’s on you. 😏
