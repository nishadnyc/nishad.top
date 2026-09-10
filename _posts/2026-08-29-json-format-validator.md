---
layout: post
title: "json-format-validator"
date: 2026-08-29 01:07:45 +0000
categories: projects
excerpt: "json‑format‑validator: Secure, Light‑Weight JSON Validation & Formatting for Node.js ! npm version..."
---

# json‑format‑validator: Secure, Light‑Weight JSON Validation & Formatting for Node.js

![npm version](https://img.shields.io/npm/v/json-format-validator.svg) ![license](https://img.shields.io/npm/l/json-format-validator.svg)

## Overview  

`json-format-validator` is a minimalistic Node.js utility that **validates, sanitizes, and pretty‑prints JSON strings** without ever throwing unhandled exceptions. It is engineered to keep your server alive even when faced with malformed or malicious payloads, making it a reliable building block for APIs, middleware, CLI tools, and Git workflows.

## Why It Matters  

JSON is the lingua franca of modern web services, but parsing user‑provided strings can introduce two major risks:

| Risk | Impact | How `json-format-validator` mitigates it |
|------|--------|-------------------------------------------|
| **Prototype Pollution** | Attackers inject `__proto__` or `constructor` keys to hijack object prototypes, potentially leading to arbitrary code execution. | Custom reviver strips `proto` and `constructor` keys during `JSON.parse`. |
| **Memory Exhaustion** | Gigantic payloads block Node’s single‑threaded event loop, causing denial‑of‑service. | Pre‑parse size check (configurable in MB) aborts oversized inputs before parsing. |

By handling errors gracefully and returning a **status + data** object, the library guarantees that your application never crashes due to a bad JSON payload.

## Core Features  

- **Safe Parsing** – Automatic removal of prototype‑polluting keys (`proto`, `constructor`).  
- **Fail‑Safe API** – Returns `{ status: boolean, data: string }`; no thrown syntax errors.  
- **Payload Guard** – Configurable maximum input size (default 5 MB) to avoid memory spikes.  
- **Flexible Indentation** – Choose spaces (0‑10) or tabs (`'-t'`) for the formatted output.  
- **Universal Import** – Works with both CommonJS (`require`) and ES Modules (`import`).  
- **CLI Support** �� Quick prettification from the terminal with `npx json-format`.  
- **Middleware Ready** – Simple Express.js middleware wrapper for request validation.  
- **Git Hook Friendly** – Validate staged `.json` files before commits to enforce repository health.

## Installation  

```bash
npm install json-format-validator
```

## API Reference  

```ts
processAndFormatJson(jsonString, [indent], [limitMb])
```

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `jsonString` | `string` | — | Raw JSON content to be processed. |
| `indent` | `number \| string` | `2` | Number of spaces (0‑10) or `'-t'` for tabs. |
| `limitMb` | `number` | `5` | Maximum allowed payload size in megabytes. |

**Return Value**

```ts
{
  status: boolean, // true = success, false = parse/validation failure
  data: string     // pretty‑printed JSON on success, original input on failure
}
```

### Security Safeguards  

- **Prototype Pollution Defense:** Custom reviver discards dangerous keys.  
- **Buffer Guard:** Input length is checked before parsing to keep the event loop responsive.

## Quick Start  

### 1. Basic Usage (CommonJS)

```js
const processAndFormatJson = require('json-format-validator');

const rawJson = '{"name":"Alice","role":"admin"}';
const result = processAndFormatJson(rawJson);

console.log(result);
// → { status: true, data: '{\n  "name": "Alice",\n  "role": "admin"\n}' }
```

### 2. ES Modules

```js
import processAndFormatJson from 'json-format-validator';

const rawJson = '{"status":"active","count":42}';
const result = processAndFormatJson(rawJson);
```

### 3. Custom Indentation & Tab Support  

```js
const formatted4Spaces = processAndFormatJson(input, 4); // 4-space indent
const formattedTabs    = processAndFormatJson(input, '-t'); // tab indent
```

### 4. Enforcing a Larger Payload Limit  

```js
// Allow up to 10 MB payloads
const result = processAndFormatJson(largeJsonString, 2, 10);
```

### 5. Graceful Error Handling  

```js
const invalidJson = '{"title": "Bug Report", status: open}';
const result = processAndFormatJson(invalidJson);

if (!result.status) {
  console.log('Failed to parse or format JSON input safely.');
  console.log('Original Input:', result.data);
}
```

## Advanced Integrations  

### Express.js Middleware  

```js
const express = require('express');
const processAndFormatJson = require('json-format-validator');

const app = express();

function validateJsonMiddleware(options = {}) {
  const { indent = 2, limitMb = 5 } = options;

  return (req, res, next) => {
    if (typeof req.body !== 'string') return next();

    const { status, data } = processAndFormatJson(req.body, indent, limitMb);
    if (!status) {
      return res.status(400).json({
        error: 'Invalid JSON payload received',
        raw: data
      });
    }

    req.formattedJson = data;
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

```bash
# Prettify a JSON file using 2‑space indentation
npx json-format config.json

# Prettify using tabs and redirect to a new file
npx json-format data.json -t > pretty-data.json
```

### Git Pre‑Commit Hook  

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

for (const file of stagedFiles) {
  const content = fs.readFileSync(file, 'utf8');
  const { status } = processAndFormatJson(content);
  if (!status) {
    console.error(`[Pre‑Commit Error] Invalid JSON syntax in file: ${file}`);
    hasError = true;
  }
}

if (hasError) process.exit(1);
```

Add the script to your `package.json` hooks (e.g., with `husky`) to block malformed JSON from entering the repository.

## Real‑World Use Cases  

- **API Gateways** – Validate external POST bodies before they hit core business logic.  
- **Microservice Communication** – Ensure inter‑service messages are well‑formed and safe.  
- **CI/CD Pipelines** – Automate JSON linting in pull‑request validation steps.  
- **Developer Tools** – Provide on‑the‑fly formatting in terminal scripts or editor plugins.  
- **Legacy System Migration** – Safely ingest large JSON dumps while protecting against malformed entries.

## Conclusion  

`json-format-validator` delivers a **secure, predictable, and developer‑friendly** approach to handling JSON payloads in Node.js environments. By combining prototype‑pollution defense, payload size guarding, and a simple yet expressive API, it lets you focus on business logic while keeping your server robust against malformed or malicious input.

---  

*License:* MIT  
*Package:* https://www.npmjs.com/package/json-format-validator  