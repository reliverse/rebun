# Reliverse Rebun

> @reliverse/rebun is a beginner-friendly wrapper around the Bun runtime API. Because Bun is fast-first — but not always beginner-first.

[📦 NPM](https://npmjs.com/package/@reliverse/rebun) • [✨ GitHub](https://github.com/reliverse/rebun) • [💬 Discord](https://discord.gg/Pb8uKbwpsJ)

## 💡 Why Rebun?

Bun is amazing: fast, native, batteries-included.

But for newer devs — or folks migrating from Node.js — its API can be inconsistent in places. **Rebun** is here to help:

- Wraps core **Bun APIs** with more **predictable** and **friendly** interfaces
- Removes gotchas around `Bun.file`, `Bun.write`, `Bun.serve`, and more
- Adds ergonomic helpers for building apps, CLIs, tools, and servers

> **⚠️ Heads up!**  
> Most of the things mentioned in this doc aren’t implemented *yet* — they’re part of the vision for `v1.0.0`.
> Got thoughts? Ideas? Complaints? Drop your feedback in [Discord](https://discord.gg/Pb8uKbwpsJ) or use [GitHub Issues](https://github.com/reliverse/reosapi/issues).
> Your feedback means the world and helps shape where this project goes next. Thank you!

## ✨ Features

- 🍰 Simpler `read`, `write`, `serve`, and `spawn` utilities
- 🧠 Fully typed (TypeScript-first)
- 📦 Drop-in replacement for most Bun APIs
- 🔥 Clean `serve()` with middleware support (like Express)
- 🪄 Automatic MIME type handling, encoding, etc.
- ⚙️ Works in **CLI tools**, **scripts**, **servers**, and **test runners**
- 🚫 No monkey-patching or shims — just ergonomic wrappers

## 📦 Installation

```bash
bun add @reliverse/rebun
# or: npm install @reliverse/rebun
```

## 🚀 Usage

```ts
import { readFile, writeFile, serve } from "@reliverse/rebun";

const text = await readFile("./hello.txt");
await writeFile("./copy.txt", text);

serve(({ req }) => {
  return new Response("Hello from Rebun!");
});
```

## 🔧 API Overview

### 📄 Files

```ts
await readFile("file.txt");            // Reads file as UTF-8 string
await readFileBuffer("image.png");     // Reads file as Uint8Array
await writeFile("out.txt", "Hello!");  // Writes string
await copyFile("a.txt", "b.txt");      // Simple copy
await removeFile("temp.log");          // Delete file
await ensureDir("logs/");              // Create dir if missing
```

### 🌐 Server

```ts
serve(({ req, url, json, text }) => {
  if (url.pathname === "/hello") return text("Hello!");
  if (url.pathname === "/json") return json({ ok: true });
  return text("404 Not Found", 404);
});
```

Supports:

- ✨ auto-parsing URL
- ⚡ `.text()`, `.json()`, `.html()` response helpers
- 🧱 static file serving (coming soon)
- 🧩 middleware (coming soon)

### 🖥 Process

```ts
const result = await run("echo Hello!");
console.log(result.stdout); // "Hello!"
```

## 🧪 Examples

### Hello World Server

```ts
import { serve } from "@reliverse/rebun";

serve(() => new Response("Hello world!"));
```

### Bun Script with Better File Handling

```ts
import { readFile, writeFile } from "@reliverse/rebun";

const data = await readFile("data.json");
await writeFile("backup.json", data);
```

## 🔮 Roadmap

- [ ] Core file utils (`readFile`, `writeFile`, etc.)
- [ ] Clean `serve()` with DX enhancements
- [ ] Built-in static file server
- [ ] `fetch()` wrappers with auto JSON, timeout, retry
- [ ] Test utilities
- [ ] CLI generator templates
- [ ] Bun plugin system support

## 👶 Who’s It For?

- 🆕 **New Bun users** who want a smoother, less quirky API surface
- 🧰 **Tool builders** and **CLI authors** who want fast bootstraps without low-level Bun fiddling
- 📝 **Script writers** tired of boilerplate just to write a simple utility
- 🔁 **Teams migrating** from Node.js or Deno, seeking familiar ergonomics
- 🔍 Developers who *don’t* want to list `bun` in `package.json`:

    > *Why?* In some setups — like when I was building [`@reliverse/relidler`](https://github.com/reliverse/relidler) — you might be **forced** to add `bun` as a dep just to pass tools like `JSR`. But that breaks tools like [`knip`](https://knip.dev) that flag unused deps. The fix? Add `"ignoreDependencies": ["bun"]` in your `knip.json`. **Or... just use `@reliverse/rebun`**, which acts as a thin wrapper with zero overhead and smooth developer ergonomics.

## 🧠 Similar Projects

- [`Bun`](https://bun.sh/docs) — official docs
- [`@reliverse/cli`](https://github.com/reliverse/cli) — CLI toolkit using Rebun
- [`@reliverse/rempts`](https://github.com/reliverse/rempts) — beautiful prompt & command system

## 💬 Community

- [💬 Join Discord](https://discord.gg/Pb8uKbwpsJ)
- [🐣 Follow @blefnk](https://twitter.com/blefnk)
- [🧙 Suggest features](https://github.com/reliverse/rebun/issues)

## 📄 License

- MIT © [blefnk Nazar Kornienko](https://github.com/blefnk)  
- Part of the [Reliverse](https://github.com/reliverse) ecosystem

*🌀 This README was proudly generated with [Remdn](https://github.com/reliverse/remdn)*
