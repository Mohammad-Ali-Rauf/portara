# 🌐 Portara

## Status: In Development

**TL;DR:** Localhost → temporary URL → share. Done.

Localhost sharing without the setup headache — one command, temporary URL, zero config nightmares.

Portara gives you ephemeral tunnels with literally one command. No accounts, no cloud signups, no YAML files to cry over. Just share and go.

```
🔒 All tunnels are end-to-end encrypted.
   Why trust me? Two reasons:
     1️⃣ I’m too broke to afford a server—so good luck finding your data on my cloud (spoiler: it doesn’t exist).
     2️⃣ I’ve got zero interest in your data—because unlike some folks, I don’t dream of federal prison. 😅
```

*("Wait, where's the setup?" There isn't any. That's the magic. 😂)*

---

## 🚨 The Problem

Trying to show your local work shouldn't require:

- Creating yet another SaaS account
- Reading 47 pages of documentation
- Configuring docker-compose files until 3AM
- Understanding networking protocols (we have lives, people)

You just want to share. Not become a DevOps engineer(I've suffered so you don't have to 😉).

---

## 💡 The Solution

> Reality Check: **only Linux is supported for now**, will add support later for windows and macos (if needed).
> 💡 Want macOS/Windows support? Do it yourself, PRs welcome.

Literally this: (copy-paste, don't overthink it) 

> Yeah, it’s on Netlify. But you can read the script in the root of this repository, ain't nobody hacking you, and netlify is only hosting the script, everything else is local.
```bash
curl -fsSL https://install.portara.netlify.app | bash  
portara expose 3000
```

Boom. You get a URL. Share it. It works. It disappears later. Your app stays on your machine.

No "set up the coordinator on your own server." No "configure the reverse proxy." No "update your DNS records." Just ✨works✨.

---

## ⚡ Here's What's Happening Under The Hood

Okay fine, for those who care: When you run that install script, it:

1. Downloads the Portara CLI
2. Spins up a lightweight local coordinator (yes, on YOUR machine)
3. Sets up encrypted tunnels between components
4. Does all the networking voodoo so you don't have to

**Your Machine (Doing Everything):**  
`CLI 🧑‍💻 ↔ 🤖 Local Coordinator ↔ 🔗 Encrypted Tunnel ↔ 🌐 Public URL`  

Dashboard (optional) -- also on your machine, because why not?

Everything runs locally. No data leaves unless you're sharing a tunnel. You're basically your own tunnel service, minus the 3-hour setup tutorial.

---

## 🧩 What’s the "Local Coordinator"?

Don’t worry, it’s not a monster.  
It's a tiny backend process that runs on your machine. All Portara clients (CLI now, a web dashboard later) connect to it locally.
Think of it as the “hub” that reduces duplicated code and keeps things reusable.

**Tech stack:**  
- CLI → TypeScript + Bun.js  
- Local Coordinator → Elysia.js  
- Dashboard/Web Client → TanStack Start  

That’s it. No rocket science, just clean architecture.

---

## 🚀 Commands

```bash
# The classics:  
portara expose <port>    # 🎯 Create a tunnel  
portara close <port>     # 🔪 Kill a tunnel  
portara list             # 📋 List active tunnels  

# The extras:  
portara config           # ⚙️ Change settings (rarely needed)

# The extras of the extras which you need only if you are either possessed or you like to copy me without understanding concepts
portara freeze <port>    # ❄️  Pause a tunnel (preserves URL, stops traffic)
portara unfreeze <port>  # 🔥 Resume a paused tunnel
```

---

## 🛠️ Programmable & Configurable

- Everything configurable in `portara.toml` (but you don't "need" to touch it but you may if you "want" to)
- Automate, script, or tweak tunnels and settings
- Power users rejoice — the CLI and dashboard are fully programmable
- *"But I just want to share localhost"* → Cool, ignore this section entirely

---

## 🏗️ Advanced Mode (Optional)

```bash
# Run just the coordinator (why though?)
# (Image not yet public — coming soon!)
docker run -p 8080:8080 mohammadalirauf/portara/coordinator  
```

But like… the curl command does this automatically. You're just making work for yourself. 😅

> Maybe someday v2 of Local Coordinator made in GraphQL instead of only REST? Just a thought. 😂

---

## ✨ Why This Doesn't Suck

- ✅ No signup — not even a "enter your email for spam"
- ✅ No credit card — not today, SaaS overlords
- ✅ No config files — unless you want them
- ✅ No persistent cloud — coordinator runs on YOUR machine
- ✅ No patience required — it works in under 10 seconds (or your localhost owes you an apology)

---

## 🎯 The Real Vibe

Portara = The "I don't have time for this shit" solution to localhost sharing. For when:

- Your designer needs to see the UI NOW
- Your client is impatient and refreshing their email
- You're testing webhooks and ngrok's free tier ran out
- You just want something that WORKS without the ceremony

*"But what about enterprise features?"* Bro, you got a temporary URL in under 10 seconds. Sometimes that's enough. 😂

---

##  🛠️ Hacking on Portara?

Clone the repo, run ```bun install```, and check ```DEVELOP.md``` (when it exists 😅).

---

## 📜 License

MIT — free, open source, hackable. The curl command just makes it easy for normal humans.

---

Try it or don't. Your localhost-sharing anxiety is your own problem. 😉
