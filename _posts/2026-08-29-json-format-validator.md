---
layout: post
title: "json-format-validator"
date: 2026-08-29 01:07:45 +0000
categories: projects
excerpt: "Securely Handling JSON with json-format-validator Handling JSON data in a Node.js environment often..."
---

# Securely Handling JSON with json-format-validator

Handling JSON data in a Node.js environment often feels like a gamble. A single malformed string can trigger a runtime syntax error that crashes your entire server, and blindly parsing user-supplied JSON opens the door to serious security vulnerabilities like Prototype Pollution.

To solve these problems, I created `json-format-validator`, a lightweight utility designed to validate, sanitize, and format JSON strings without the risk of unhandled exceptions.

[![npm version](https://img.shields.io/npm/v/json-format-validator.svg)](https://www.npmjs.com/package/json-format-validator)
[![license](https://img.shields.io/npm/l/json-format-validator.svg)](LICENSE)

## What is json-format-validator?

`json-format-validator` is a fail-safe wrapper for JSON processing. Instead of using `JSON.parse()` and `JSON.stringify()` directly—which can throw errors or be exploited—my utility wraps these processes in a secure layer. 

The primary goal is to ensure that no matter what string is passed into the function, the server remains stable and the data remains clean.

## Key Features

### 1. Safe Parsing & Security
Security is at the core of this project. I have implemented a defense mechanism against **Prototype Pollution** by stripping sensitive prototype keys (`__proto__` and `constructor`) during the parsing phase. This prevents attackers from injecting properties into the global object prototype.

### 2. Fail-Safe Response Pattern
I designed the utility to avoid throwing runtime exceptions. Instead of a `try-catch` block in your business logic, the utility returns a consistent status object:
* `{ status: true, data: 'formatted-json' }` on success.
* `{ status: false, data: 'original-input' }` on failure.

### 3. Payload Guard
To protect against memory exhaustion attacks (DoS), I've included a configurable size limit. By default, the utility limits payloads to 5 MB, ensuring that oversized strings don't block the Node.js event loop.

### 4. Flexible Formatting
Formatting is highly customizable. I provide support for:
* **Space-based indentation:** Configurable from 0 to 10 spaces.
* **Tab-based indentation:** Simply pass `'-t'` to use tabs.

## Practical Use Cases

### API Middleware (Express.js)
I often use this as middleware to sanitize incoming raw payloads before they reach my route handlers. This ensures that only valid, sanitized JSON enters the application logic.

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
      return res.status(400).json({
        error: 'Invalid JSON payload received',
        raw: result.data
      });
    }

    req.formattedJson = result.data;
    next();
  };
}
```

### Git Pre-commit Hooks
To maintain a clean codebase, I use the utility in pre-commit scripts to prevent invalid `.json` files from being committed to the repository.

### Command-Line Tooling
For those who prefer the terminal, I've included CLI support. You can quickly prettify files using `npx`:

```bash
# Prettify with 2 spaces
npx json-format config.json

# Prettify using tabs and save to a file
npx json-format data.json -t > pretty-data.json
```

## Quick Start

Installation is straightforward:

```bash
npm install json-format-validator
```

Whether you use CommonJS or ES Modules, the integration is seamless:

```javascript
import processAndFormatJson from 'json-format-validator';

const rawJson = '{"name":"Alice","role":"admin"}';
const result = processAndFormatJson(rawJson);

if (result.status) {
  console.log('Success:', result.data);
}
```

By combining security safeguards with a fail-safe API, `json-format-validator` removes the anxiety of handling external JSON data in Node.js applications.