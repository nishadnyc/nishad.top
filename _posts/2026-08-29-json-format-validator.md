---
layout: post
title: "json-format-validator"
date: 2026-08-29 01:07:45 +0000
categories: projects
excerpt: "json‑format‑validator: A Safe, Zero‑Crash JSON Sanitizer & Pretty‑Printer for Node.js ! npm version..."
---

# json‑format‑validator: A Safe, Zero‑Crash JSON Sanitizer & Pretty‑Printer for Node.js

![npm version](https://img.shields.io/npm/v/json-format-validator.svg) ![license](https://img.shields.io/npm/l/json-format-validator.svg)

When a Node.js service receives raw JSON from external sources—webhooks, API clients, Git hooks—any malformed payload or malicious prototype pollution can bring an entire server down. **json‑format‑validator** eliminates those risks. It parses, sanitizes, and formats JSON strings without ever throwing uncaught exceptions, returning a clean status object that tells you exactly what happened.

---

## Why You Need a Dedicated JSON Guard

| Threat | What Happens Without a Guard | How json‑format‑validator Helps |
|--------|--------------------------------|--------------------------------|
| **Syntax Errors** | `JSON.parse` throws, crashing the request handler. | Returns `{ status: false, data: rawInput }` instead of throwing. |
| **Prototype Pollution** | `{"__proto__": {"admin": true}}` can corrupt the global prototype chain. | Strips `__proto__`, `proto`, and `constructor` keys during parsing. |
| **Memory Exhaustion** | Huge payloads (hundreds of MB) block the event loop. | Enforces configurable payload size limits (default 5 MB). |
| **Inconsistent Indentation** | Hand‑crafted JSON may be hard to read in logs. | Outputs pretty‑printed JSON with 0‑10 spaces or tabs. |

---

## Core Features at a Glance

- **Safe Parsing** – Custom reviver removes prototype‑polluting keys.
- **Fail‑Safe Response** – Always returns a plain object `{ status, data }`.
- **Payload Guard** – Set a maximum payload size in megabytes.
- **Flexible Indentation** – Choose spaces (0‑10) or tab (`'-t'`) formatting.
- **Universal Import** – Works with both CommonJS (`require`) and ES Modules (`import`).
- **CLI Support** – Prettify files directly from the terminal.
- **Express Middleware** – Plug‑and‑play validation for incoming HTTP bodies.
- **Git Pre‑commit Hook** – Prevent bad JSON from entering your repository.

---

## Quick Start

```bash
npm install json-format-validator
```

### Basic Usage (CommonJS)

```js
const processAndFormatJson = require('json-format-validator');

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

### ES Modules

```js
import processAndFormatJson from 'json-format-validator';

const raw = '{"status":"active","count":42}';
const { status, data } = processAndFormatJson(raw);
```

---

## Advanced Formatting Options

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `indent` | `number` |0‑10 or `'-t'` | Number of spaces per level, or `'-t'` for tabs. |
| `limitMb` | `number` | `5` | Maximum payload size in megabytes. |

```js
// 4‑space indentation
processAndFormatJson('{"debug":true,"level":3}', 4);

// Tab indentation
processAndFormatJson('{"debug":true,"level":3}', '-t');
```

### Custom Size Limits

```js
// Allow up to 10 MB payloads, use 2‑space indentation
processAndFormatJson(largeJsonString, 2, 10);
```

---

## Handling Errors Gracefully

When parsing fails—due to invalid syntax, wrong type, or size breach—the function never throws. Instead, `status` is `false` and `data` contains the untouched input for logging or debugging.

```js
const invalidJson = '{"title": "Bug Report", status: open}';
const result = processAndFormatJson(invalidJson);

if (!result.status) {
  console.log('Failed to parse or format JSON safely.');
  console.log('Original Input:', result.data);
}
```

---

## Real‑World Integrations

### 1. Express.js Middleware

Validate and sanitize incoming JSON bodies before they hit your route logic.

```js
const express = require('express');
const processAndFormatJson = require('json-format-validator');

const app = express();

function validateJsonMiddleware(options = {}) {
  const { indent = 2, limitMb = 5 } = options;
  return (req, res, next) => {
    if (typeof req.body !== 'string') return next();

    const result = processAndFormatJson(req.body, indent, limitMb);
    if (!result.status) {
      return res.status(400).json({
        error: 'Invalid JSON payload received',
        raw: result.data
      });
    }
    req.formattedJson = result.data;
    next();
  };
}

app.post(
  '/api/webhook',
  express.text({ type: '*/*', limit: '5mb' }), // raw text body
  validateJsonMiddleware(),
  (req, res) => {
    res.send(`Received valid JSON:\n${req.formattedJson}`);
  }
);
```

### 2. Command‑Line Interface (CLI)

Prettify JSON files directly from a terminal, useful for ad‑hoc debugging or CI pipelines.

```bash
# Pretty‑print with 2 spaces
npx json-format config.json

# Use tabs and redirect output
npx json-format data.json -t > pretty-data.json
```

### 3. Git Pre‑commit Hook

Stop malformed JSON from being committed.

```js
// check-json.js
const { execSync } = require('child_process');
const fs = require('fs');
const processAndFormatJson = require('json-format-validator');

const staged = execSync('git diff --cached --name-only --diff-filter=ACM "*.json"')
  .toString()
  .trim()
  .split('\n')
  .filter(Boolean);

let hasError = false;
staged.forEach(file => {
  const content = fs.readFileSync(file, 'utf8');
  const result = processAndFormatJson(content);
  if (!result.status) {
    console.error(`[Pre‑Commit Error] Invalid JSON syntax in file: ${file}`);
    hasError = true;
  }
});

if (hasError) process.exit(1);
```

Add the script to your `.git/hooks/pre-commit` file and you’ll never commit broken JSON again.

---

## API Reference

```ts
processAndFormatJson(
  jsonString: string,
  indent?: number | string,   // 0‑10 or '-t'
  limitMb?: number            // default 5 MB
) => { status: boolean, data: string }
```

- **`jsonString`** – Raw JSON string to validate.  
- **`indent`** – Desired indentation (spaces) or `'-t'` for tab characters.  
- **`limitMb`** – Upper bound for the payload size, protecting the event loop.

**Return object**

| Property | Type | Meaning |
|----------|------|---------|
| `status` | `boolean` | `true` if parsing and formatting succeeded; otherwise `false`. |
| `data`   | `string`  | Pretty‑printed JSON on success, or the original input on failure. |

---

## Security Safeguards in Detail

1. **Prototype Pollution Defense**  
   A custom reviver removes any `__proto__`, `proto`, or `constructor` keys **before** the object is constructed, neutralizing attempts to tamper with the JavaScript prototype chain.

2. **Buffer Guard**  
   The function checks the byte length of the input against the `limitMb` option. If the payload exceeds the limit, processing stops early—preventing the single‑threaded Node.js event loop from being blocked.

Both safeguards are built into the core parsing routine, so you get protection *without* extra configuration.

---

## When to Use json‑format‑validator

- **Public APIs & Webhooks** – Safely accept JSON from unknown clients.
- **Microservices** – Guard internal message queues or event streams.
- **CI / CD Pipelines** – Enforce JSON linting before deployment.
- **Developer Tools** – Quickly pretty‑print JSON in the terminal.
- **Legacy Systems** – Add a thin validation layer without refactoring existing parsers.

---

## Getting Involved

The package is released under the **MIT** license, making it free for commercial and open‑source projects alike. Contributions, issue reports, and feature requests are welcome on the GitHub repository.

---

**Take control of JSON handling today—replace brittle `JSON.parse` calls with a resilient, secure validator that never crashes your server.**