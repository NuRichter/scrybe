<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:07070a,55:6b4f1d,100:c8973a&height=200&section=header&text=Scrybe%20Web&fontColor=f4e3b2&fontSize=66&fontAlignY=36&desc=The%20launcher%20site%20for%20Scrybe%20.%20deploy%20it%20on%20Vercel%20in%20seconds&descAlignY=58&descSize=16" alt="Scrybe Web">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Next.js-14-07070a?style=for-the-badge&logo=nextdotjs&logoColor=c8973a" alt="Next.js 14">
  <img src="https://img.shields.io/badge/TypeScript-strict-07070a?style=for-the-badge&logo=typescript&logoColor=c8973a" alt="TypeScript">
  <img src="https://img.shields.io/badge/Tailwind-3-07070a?style=for-the-badge&logo=tailwindcss&logoColor=c8973a" alt="Tailwind">
  <img src="https://img.shields.io/badge/Deploy-Vercel-07070a?style=for-the-badge&logo=vercel&logoColor=c8973a" alt="Vercel">
  <img src="https://img.shields.io/badge/A%20NuRichter%20Workspace%20Tool-c8973a?style=for-the-badge&labelColor=07070a" alt="NuRichter Workspace">
</p>

<h3 align="center">The launcher for Scrybe. Paste a link, take a command.</h3>

---

## What this is

This is the website for **Scrybe**, the Scribd to PDF tool by NuRichter Workspace. Let me be straight with you, because that is the only way I talk.

Scribd hits cloud and datacenter IPs with a CAPTCHA. That means a website hosted on Vercel cannot pull documents on its own, no matter how clever the server code is. It would hit a CAPTCHA wall every single time. Anyone who tells you otherwise has not actually tried it.

So this site does the honest thing that actually works. It talks to a small local server, the **Scrybe bridge**, that runs on your machine with your IP and your Chrome. That is the connection Scribd does not challenge. The flow:

- you start the bridge once on your machine
- you paste a Scribd link on the site and hit process
- the site hands the job to the bridge at `http://127.0.0.1:8787`
- the bridge prints the PDF, zips it with a manifest, and streams it back
- the zip lands in your downloads, with live progress the whole way

Browsers allow an HTTPS page to reach `127.0.0.1`, so the deployed site drives a local engine cleanly. If the bridge is not running, the site says so plainly and shows you how to start it.

> The bridge and the CLI engine live in the [Scrybe repo](https://github.com/NuRichter/scrybe). This is the front door.

---

## The stack

- **Next.js 16** App Router, fully static, no backend on Vercel
- **React 19** and **TypeScript 6**, strict
- **Tailwind CSS 4**, CSS first theme, industrial blueprint tokens
- Talks to the local **Scrybe bridge** over a streamed NDJSON protocol
- **lucide-react 1.x** for icons, with an inline mark where lucide dropped brand glyphs
- Display type Rajdhani, technical type JetBrains Mono, body DM Sans

---

## Run it locally

```bash
git clone https://github.com/NuRichter/scrybe-web.git
cd scrybe-web
npm install
npm run dev
```

Open `http://localhost:3000`. Done. That is the whole setup.

To check the production build before you ship:

```bash
npm run build
```

---

## Deploy on Vercel

This is the easy part. I built it to be the easy part.

1. Push this repo to your GitHub.
2. Go to Vercel, click New Project, import the repo.
3. Leave every setting on default. Vercel detects Next.js on its own.
4. Click Deploy.

That is it. No environment variables. No build tweaks. No drama. In about a minute you have a live URL.

To make the process button work, the visitor runs the Scrybe bridge on their own machine. The site looks for it at `http://127.0.0.1:8787`. Bridge instructions live in the [Scrybe repo](https://github.com/NuRichter/scrybe). If the bridge is offline, the site explains the steps in place, so a deploy without the bridge still reads honestly instead of throwing a dead button.

Prefer the command line?

```bash
npm i -g vercel
vercel
```

---

## Make it yours

- **Brand colors** live in `tailwind.config.ts`. The gold is `#c8973a`, the void is `#07070a`. Change them once, the whole site follows.
- **Copy and content** live in `lib/content.ts`. Pipeline steps, spec, env vars, field notes, terminal lines. Edit text there, not in the components.
- **The link logic** lives in `lib/scrybe.ts`. It mirrors the Python tool exactly, so what the site shows is what the tool will do.
- **GitHub links** point at `github.com/NuRichter/scrybe`. Search and replace if your handle differs.

---

## Project shape

```
app/            layout, page, theme, favicon
components/     every section, Forge talks to the bridge, plus helpers
lib/            scrybe.ts (link logic), content.ts (copy)
hooks/          useReveal (scroll animation)
public/         scribd mark
```

The bridge URL is set at the top of `components/Forge.tsx` as `BRIDGE`. Change the port there if you run the bridge on something other than 8787.

Clean files. No comments. The code says what it does by saying it plainly.

---

## License

MIT. Do what you want, just keep the notice. See [LICENSE](LICENSE).

Scrybe is a rebranded fork of the open source Scribd Downloader by Usama Nazir, also MIT. Credit stays where credit is due.

---

## Disclaimer

Read this part. The tool is for educational purposes. Respect copyright law and respect Scribd Terms of Service. Only handle documents you have the right to access. What you do with it is on you, not on NuRichter Workspace.

---

<p align="center">
  Built and maintained by <a href="https://github.com/NuRichter"><b>NuRichter</b></a> . NuRichter Workspace
</p>

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:c8973a,45:6b4f1d,100:07070a&height=120&section=footer" alt="footer">
</p>
