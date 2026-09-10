---
layout: post
title: "json-format-validator"
date: 2026-08-29 01:07:45 +0000
categories: projects
excerpt: "json‑format‑validator: Secure, Fail‑Safe JSON Validation & Formatting for Node.js ! npm version (ht..."
---

# json‑format‑validator: Secure, Fail‑Safe JSON Validation & Formatting for Node.js

![npm version](https://img.shields.io/npm/v/json-format-validator.svg) ![license](https://img.shields.io/npm/l/json-format-validator.svg)

## Why a Dedicated JSON Validator?

JSON is the lingua franca of modern web APIs, but parsing raw strings in a Node.js server still carries hidden risks:

| Threat | What Happens | How **json‑format‑validator** Helps |
|--------|--------------|------------------------------------|
| **Prototype Pollution** | Malicious payloads inject `__proto__` or `constructor` keys, corrupting the global object prototype. | The parser strips those keys during parsing, neutralizing the attack. |
| **Denial‑of‑Service via Huge Payloads** | Unchecked `JSON.parse` on multi‑megabyte strings blocks the event loop. | A configurable size guard aborts parsing before the memory budget is exceeded. |
| **Unhandled Exceptions** | Syntax errors cause uncaught exceptions that can crash the process. | The library returns a structured `{ status, data }` object instead of throwing. |

By wrapping these safeguards into a tiny utility, you get peace of mind without sacrificing developer ergonomics.

---

## Core Features at a Glance

- **Safe Parsing** – Automatic removal of `__proto__` and `constructor` keys.
- **Fail‑Safe API** – Always returns `{ status: boolean, data: string }`; no thrown errors.
- **Payload Guard** – Enforces a configurable size limit (default 5 MB) to stop memory‑exhaustion attacks.
- **Flexible Indentation** – Choose 0‑10 spaces or switch to tabs (`'-t'`).
- **Universal Import** – Works with CommonJS (`require`) **and** ES Modules (`import`).
- **CLI & Git Hook Support** – Prettify files from the terminal or reject bad JSON before commits.
- **Express Middleware** – Validate inbound request bodies with a single plug‑in.

---

## Installation

```bash
npm install json-format-validator
```

The package is published on npm and works with any Node.js version supporting ES2020+.

---

## Getting Started

### 1. Basic Usage – CommonJS

```js
// commonjs-example.js
const processAndFormatJson = require('json-format-validator');
// Or destructure the named export:
const { processAndFormatJson } = require('json-format-validator');

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

### 2. ES Modules

```js
// es-modules-example.mjs
import processAndFormatJson from 'json-format-validator';
// Or named import:
import { processAndFormatJson } from 'json-format-validator';

const rawJson = '{"status":"active","count":42}';
const { status, data } = processAndFormatJson(rawJson);
console.log(status, data);
```

Both styles return the same safe, pretty‑printed payload.

---

## Custom Indentation & Tab Support

Control the visual formatting of the output:

```js
const processAndFormatJson = require('json-format-validator');

const input = '{"debug":true,"level":3}';

// 4‑space indentation
const formatted4 = processAndFormatJson(input, 4);
console.log(formatted4.data);

// Tab indentation (use the literal string '-t')
const formattedTabs = processAndFormatJson(input, '-t');
console.log(formattedTabs.data);
```

Valid indentation values are integers `0–10` (spaces) or the string `'-t'` for tabs.

---

## Enforcing Payload Size Limits

When dealing with large uploads, set a safety ceiling in megabytes:

```js
// Allow up to 10 MB payloads
const result = processAndFormatJson(largeJsonString, 2, 10);
if (!result.status) {
  console.warn('Payload too large or malformed');
}
```

The third argument (`limitMb`) defaults to **5 MB** if omitted.

---

## Graceful Error Handling

If parsing fails, the library never throws. Instead, `status` becomes `false` and `data` contains the original input.

```js
const processAndFormatJson = require('json-format-validator');

const badJson = '{"title": "Bug Report", status: open}';
const result = processAndFormatJson(badJson);

if (!result.status) {
  console.error('Invalid JSON');
  console.error('Raw input retained:', result.data);
}
```

This pattern keeps your server running and lets you surface clear error messages to callers.

---

## Advanced Integrations

### Express Middleware

```js
const express = require('express');
const processAndFormatJson = require('json-format-validator');

const app = express();

function validateJsonMiddleware(opts = {}) {
  const { indent = 2, limitMb = 5 } = opts;
  return (req, res, next) => {
    if (typeof req.body !== 'string') return next();

    const { status, data } = processAndFormatJson(req.body, indent, limitMb);
    if (!status) {
      return res.status(400).json({
        error: 'Invalid JSON payload received',
        raw: data,
      });
    }
    req.formattedJson = data;
    next();
  };
}

// Accept raw text bodies (e.g., webhook payloads)
app.post(
  '/api/webhook',
  express.text({ type: '*/*', limit: '5mb' }),
  validateJsonMiddleware(),
  (req, res) => {
    res.send(`Received valid JSON:\n${req.formattedJson}`);
  }
);

app.listen(3000, () => console.log('Server listening on :3000'));
```

The middleware sanitizes the body, enforces size limits, and injects the formatted JSON into `req.formattedJson`.

### Command‑Line Interface (CLI)

You can prettify JSON files directly from the terminal—no code required.

```bash
# Prettify using the default 2‑space indentation
npx json-format config.json

# Prettify using tabs and redirect output
npx json-format data.json -t > pretty-data.json
```

The CLI respects the same size guard and sanitization logic as the programmatic API.

### Git Pre‑Commit Hook

Automatically reject malformed JSON before it lands in your repository.

```js
// .git/hooks/pre-commit (make it executable)
const { execSync } = require('child_process');
const fs = require('fs');
const processAndFormatJson = require('json-format-validator');

const staged = execSync('git diff --cached --name-only --diff-filter=ACM "*.json"')
  .toString()
  .trim()
  .split('\n')
  .filter(Boolean);

let hasError = false;

for (const file of staged) {
  const content = fs.readFileSync(file, 'utf8');
  const { status } = processAndFormatJson(content);
  if (!status) {
    console.error(`[Pre‑Commit] Invalid JSON in ${file}`);
    hasError = true;
  }
}

if (hasError) process.exit(1);
```

Integrating this script into `package.json` scripts or Husky hooks enforces clean JSON across the team.

---

## API Reference

| Signature | Description |
|------------|--------------|
| `processAndFormatJson(jsonString, [indent], [limitMb])` | Parses, sanitizes, and pretty‑prints a JSON string. |
| **Parameters** | |
| `jsonString` | **string** – Raw JSON input (required). |
| `indent` | **number** (0‑10) *or* **string** `'-t'`. Default `2`. Controls spacing or tab usage. |
| `limitMb` | **number** – Maximum payload size in megabytes. Default `5`. |
| **Returns** | **Object** `{ status: boolean, data: string }` |
| `status` | `true` if parsing succeeded; `false` otherwise. |
| `data` | Formatted JSON on success; raw input on failure. |

### Security Safeguards

- **Prototype Pollution Defense** – A custom reviver strips any `__proto__` or `constructor` properties during `JSON.parse`.
- **Buffer Guard** – Byte length is measured **before** parsing; inputs exceeding `limitMb` are rejected early.

---

## When to Use json‑format‑validator

- **API Gateways** that need to validate and clean inbound JSON payloads without risking a crash.
- **Microservices** where a single malformed request should not bring down the entire process.
- **CI/CD Pipelines** that enforce code‑base hygiene by rejecting broken JSON files.
- **Developer Tooling** for quick, safe JSON pretty‑printing from the command line.
- **Legacy Systems** where you cannot fully control client inputs but still want robust sanitization.

---

## License

`json-format-validator` is released under the **MIT License**, allowing unrestricted use in both open‑source and commercial projects.

---

## Closing Thoughts

Handling JSON safely is no longer a lofty aspiration—it's a practical necessity. By integrating **json‑format‑validator** you gain:

- **Zero‑crash guarantees** (no uncaught `SyntaxError`s),
- **Built‑in defense** against prototype pollution,
- **Configurable resource limits**, and
- **A clean, consistent API** across environments.

Add it to your Node.js toolbox today and let your services focus on business logic, not on defensive parsing.