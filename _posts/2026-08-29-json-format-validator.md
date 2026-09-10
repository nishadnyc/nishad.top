---
layout: post
title: "json-format-validator"
date: 2026-08-29 01:07:45 +0000
categories: projects
excerpt: "json‑format‑validator – Safe, Simple JSON Sanitization & Pretty‑Printing ! npm version (https://img..."
---

# json‑format‑validator – Safe, Simple JSON Sanitization & Pretty‑Printing

![npm version](https://img.shields.io/npm/v/json-format-validator.svg) ![license](https://img.shields.io/npm/l/json-format-validator.svg)

When I work on backend services, I constantly receive JSON payloads from clients, webhooks, or third‑party APIs. A single malformed or malicious JSON string can crash a Node.js process, expose prototype‑pollution vulnerabilities, or overload the event loop with a gigantic payload. That’s why I created **json‑format‑validator**, a lightweight utility that validates, sanitizes, and formats JSON strings **without ever throwing an unhandled exception**.

---

## What the Project Does

`json-format-validator` takes a raw JSON string, parses it safely, strips dangerous prototype keys, enforces an optional size ceiling, and returns a nicely indented JSON string. Instead of throwing, it always returns a predictable response object:

```js
{
  status: true,   // false if parsing/validation failed
  data:   '{\n  "key": "value"\n}' // prettified JSON on success, raw input on failure
}
```

---

## Why I Built It

* **Robustness** – Node’s native `JSON.parse` throws on syntax errors, which can crash your server if not caught. My wrapper catches everything and gives you a clean status flag.  
* **Security** – Prototype‑pollution attacks target the `__proto__` and `constructor` properties. The library’s custom reviver removes those keys before they ever reach your code.  
* **Resource Guarding** – Large payloads can exhaust memory. I added a configurable payload limit (default **5 MB**) that aborts parsing early.  
* **Zero‑Configuration** – Works out‑of‑the‑box with both CommonJS (`require`) and ES Modules (`import`).  

---

## Key Features

| Feature | What It Means for You |
|---------|-----------------------|
| **Safe Parsing** | Strips `__proto__`, `proto`, and `constructor` keys during parse. |
| **Fail‑Safe Response** | Returns `{ status, data }` instead of throwing. |
| **Payload Guard** | Enforces a maximum size in megabytes (default 5 MB). |
| **Flexible Indentation** | Choose 0‑10 spaces or tabs (`'-t'`). |
| **Universal Import** | Works with `require` **and** `import`. |
| **CLI Support** | Prettify files directly from the terminal (`npx json-format`). |
| **Express Middleware** | Plug‐and‑play validation for incoming requests. |
| **Git Hook Integration** | Block invalid JSON from entering your repository. |

---

## Installation

```bash
npm install json-format-validator
```

That’s it – the package ships with a tiny runtime footprint and no peer dependencies.

---

## Quick Start

### 1. CommonJS (require)

```js
const processAndFormatJson = require('json-format-validator');
// or named import
// const { processAndFormatJson } = require('json-format-validator');

const rawJson = '{"name":"Alice","role":"admin"}';
const result = processAndFormatJson(rawJson);

console.log(result);
/*
{
  status: true,
  data: '{\n  "name": "Alice",\n  "role": "admin"\n}'
}
*/
```

### 2. ES Modules (import)

```js
import processAndFormatJson from 'json-format-validator';
// or named import
// import { processAndFormatJson } from 'json-format-validator';

const rawJson = '{"status":"active","count":42}';
const { status, data } = processAndFormatJson(rawJson);
```

---

## Advanced Usage

### Custom Indentation & Tab Support

```js
const processAndFormatJson = require('json-format-validator');

const input = '{"debug":true,"level":3}';

// 4‑space indentation
const formatted4 = processAndFormatJson(input, 4);
console.log(formatted4.data);

// Tab indentation
const formattedTabs = processAndFormatJson(input, '-t');
console.log(formattedTabs.data);
```

### Configurable Payload Limits

```js
// Allow up to 10 MB payloads
const result = processAndFormatJson(largeJsonString, 2, 10);
```

### Graceful Error Handling

```js
const invalidJson = '{"title":"Bug Report", status: open}';
const result = processAndFormatJson(invalidJson);

if (!result.status) {
  console.warn('Failed to parse JSON safely.');
  console.log('Original input was left untouched:', result.data);
}
```

---

## Integrations

### Express.js Middleware

Secure incoming webhook bodies before they hit your route logic:

```js
const express = require('express');
const processAndFormatJson = require('json-format-validator');

const app = express();

function validateJsonMiddleware({ indent = 2, limitMb = 5 } = {}) {
  return (req, res, next) => {
    if (typeof req.body !== 'string') return next();

    const result = processAndFormatJson(req.body, indent, limitMb);
    if (!result.status) {
      return res.status(400).json({
        error: 'Invalid JSON payload received',
        raw: result.data,
      });
    }

    req.formattedJson = result.data;
    next();
  };
}

app.post(
  '/api/webhook',
  express.text({ type: '*/*', limit: '5mb' }),
  validateJsonMiddleware(),
  (req, res) => {
    res.send(`Received valid JSON:\n${req.formattedJson}`);
  }
);
```

### Command‑Line Interface (CLI)

Prettify files without writing any JavaScript:

```bash
# Pretty‑print using 2 spaces
npx json-format config.json

# Use tabs and redirect output
npx json-format data.json -t > pretty-data.json
```

### Git Pre‑Commit Hook

Prevent malformed JSON from ever reaching your repository:

```js
// check-json.js
const { execSync } = require('child_process');
const fs = require('fs');
const processAndFormatJson = require('json-format-validator');

const stagedFiles = execSync('git diff --cached --name-only --diff-filter=ACM "*.json"')
  .toString()
  .trim()
  .split('\n')
  .filter(Boolean);

let hasError = false;

stagedFiles.forEach(file => {
  const content = fs.readFileSync(file, 'utf8');
  const result = processAndFormatJson(content);
  if (!result.status) {
    console.error(`[Pre‑Commit Error] Invalid JSON in ${file}`);
    hasError = true;
  }
});

if (hasError) process.exit(1);
```

Add this script to your `package.json` hooks (e.g., via `husky`) and you’ll catch bad JSON before anyone can commit it.

---

## API Reference

```ts
processAndFormatJson(
  jsonString: string,
  indent?: number | string, // 0‑10 spaces or '-t' for tabs (default 2)
  limitMb?: number           // max payload in MB (default 5)
): { status: boolean, data: string }
```

* `status` – `true` when parsing and formatting succeeded; `false` otherwise.  
* `data` – Formatted JSON on success, the untouched input on failure.

---

## Security Safeguards

### Prototype Pollution Defense
During `JSON.parse`, a custom reviver removes any key that matches:
* `__proto__`
* `proto`
* `constructor`

This neutralizes attempts to mutate `Object.prototype` and inject malicious behavior.

### Buffer Guard
Before parsing, the library measures the byte length of the input. If it exceeds the configured limit, parsing is aborted and `{ status: false }` is returned, protecting the single‑threaded Node.js event loop from memory‑exhaustion attacks.

---

## Potential Use Cases

* **API Gateways** – Validate external webhook payloads or client‑submitted JSON before processing.
* **Microservice Communication** – Ensure internal messages are well‑formed and safe.
* **CI/CD Pipelines** – Enforce JSON correctness in config files, OpenAPI specs, or translation bundles.
* **CLI Tooling** – Offer developers a quick way to prettify and sanity‑check JSON files locally.
* **Legacy Systems** – Wrap existing parsers with a fail‑safe layer without refactoring the whole codebase.

---

## Closing Thoughts

I built **json‑format‑validator** because I wanted a single, tiny dependency that could **protect** my services, **simplify** JSON handling, and **avoid** the noisy try/catch boilerplate that normally surrounds `JSON.parse`. Whether you’re writing a server, a command‑line utility, or a Git hook, this library gives you a predictable, secure, and configurable way to work with JSON—**no crashes, no prototype hijacking, just clean data**. Give it a spin and let me know how it improves your workflow!