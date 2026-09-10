---
layout: post
title: "json-format-validator"
date: 2026-08-29 01:07:45 +0000
categories: projects
excerpt: "Ensuring JSON Integrity: Introducing json-format-validator When building Node.js applications, hand..."
---

# Ensuring JSON Integrity: Introducing json-format-validator

When building Node.js applications, handling JSON is an everyday task. However, relying on a simple `JSON.parse()` can be dangerous. A single malformed string can throw an unhandled exception and crash your entire server, while maliciously crafted payloads can expose your application to Prototype Pollution attacks.

To solve these challenges, I created **json-format-validator**, a lightweight and secure utility designed to validate, sanitize, and format JSON strings without risking application stability.

![npm version](https://img.shields.io/npm/v/json-format-validator.svg)
![license](https://img.shields.io/npm/l/json-format-validator.svg)

## What is json-format-validator?

The core purpose of this project is to provide a "fail-safe" wrapper around JSON processing. Instead of letting your application crash when it encounters invalid syntax or an oversized payload, my utility intercepts these issues and returns a clean status object. 

It doesn't just check if the JSON is valid; it actively sanitizes the input and prettifies the output, making it an ideal tool for APIs, logging systems, and CI/CD pipelines.

## Key Features

### 🛡️ Security-First Parsing
I have integrated specific safeguards to protect servers from common vulnerabilities:
*   **Prototype Pollution Defense:** The utility uses custom reviver logic during parsing to strip `__proto__` and `constructor` keys, neutralizing object prototype injection attempts.
*   **Payload Guard:** To prevent memory exhaustion (DoS) attacks, I've implemented a configurable size limit (defaulting to 5 MB). The utility checks the byte length before parsing to ensure the Node.js event loop isn't blocked by oversized strings.

### 🚀 Stability and Flexibility
*   **Fail-Safe Responses:** You will never have to wrap this utility in a `try-catch` block. It returns a consistent `{ status, data }` object. If parsing fails, `status` is `false` and `data` contains the original raw input.
*   **Customizable Formatting:** You can control the visual output by specifying indentation (0–10 spaces) or by using `'-t'` for tab-based formatting.
*   **Universal Compatibility:** I've ensured the project works seamlessly across both CommonJS (`require`) and ES Modules (`import`).

## Use Cases and Integration

### 1. API Middleware
One of the most powerful ways to use this utility is as Express.js middleware. I can intercept raw payloads before they reach the route handlers to ensure only sanitized, valid JSON is processed.

```javascript
const express = require('express');
const processAndFormatJson = require('json-format-validator');
const app = express();

function validateJsonMiddleware(options = {}) {
  const { indent = 2, limitMb = 5 } = options;
  return (req, res, next) => {
    if (typeof req.body !== 'string') return next();

    const result = processAndFormatJson(req.body, indent, limitMb);
    if (!result.status) {
      return res.status(400).json({ error: 'Invalid JSON payload received', raw: result.data });
    }
    req.formattedJson = result.data;
    next();
  };
}
```

### 2. Git Pre-commit Hooks
To keep a codebase clean, I use this utility in Git hooks to prevent developers from committing malformed `.json` files. By scanning staged files through `json-format-validator`, the commit process is blocked if any syntax errors are found.

### 3. Command-Line Prettifying
For quick tasks, I've included a CLI. You can prettify files directly from the terminal using `npx`:

```bash
# Prettify a JSON file using 2 spaces
npx json-format config.json

# Prettify using tabs and save output to a new file
npx json-format data.json -t > pretty-data.json
```

## Quick Start

Installation is straightforward via npm:

```bash
npm install json-format-validator
```

**Basic Usage:**

```javascript
const processAndFormatJson = require('json-format-validator');

const rawJson = '{"name":"Alice","role":"admin"}';
const result = processAndFormatJson(rawJson);

console.log(result);
// Output: { status: true, data: '{\n "name": "Alice",\n "role": "admin"\n}' }
```

By combining security safeguards with a predictable API, `json-format-validator` removes the anxiety of handling external JSON data in Node.js environments.