---
layout: post
title: "json-format-validator"
date: 2026-08-29 01:07:45 +0000
categories: projects
excerpt: "Ensuring JSON Integrity with json-format-validator Handling JSON data is a fundamental part of mode..."
---

# Ensuring JSON Integrity with json-format-validator

Handling JSON data is a fundamental part of modern web development, but it comes with hidden risks. From runtime syntax errors that can crash a Node.js server to sophisticated security vulnerabilities like Prototype Pollution, the process of parsing external strings is often more dangerous than it seems.

To solve this, I created **json-format-validator**: a lightweight, secure utility designed to validate, sanitize, and format JSON strings without the risk of unhandled exceptions.

[![npm version](https://img.shields.io/npm/v/json-format-validator.svg)](https://www.npmjs.com/package/json-format-validator)
[![license](https://img.shields.io/npm/l/json-format-validator.svg)](LICENSE)

## Why I Built This Utility

Most developers rely on `JSON.parse()`, but that method throws a hard error if the input is malformed. If you forget a `try-catch` block, your entire application crashes. Beyond crashes, standard parsing is susceptible to "Prototype Pollution," where malicious actors inject `__proto__` or `constructor` keys to alter the behavior of your JavaScript objects.

I wanted a tool that treats JSON parsing as a fallible operation—returning a status instead of throwing an error—while baking security safeguards directly into the process.

## Key Features

### 🛡️ Security-First Parsing
I have implemented a custom reviver logic during the parsing phase to automatically strip sensitive prototype keys. By removing `__proto__` and `constructor` keys, the utility neutralizes object prototype injection attempts before the data ever reaches your business logic.

### 🚫 Fail-Safe Responses
Instead of risking a server crash, the utility returns a clean status object: `{ status, data }`. 
- If the JSON is valid, `status` is `true` and `data` contains the formatted string.
- If the JSON is invalid, `status` is `false` and `data` returns the raw input unchanged.

### 📉 Payload Guard
To protect against memory exhaustion attacks (DoS), I included a configurable payload size limit. By default, it limits inputs to 5 MB, preventing oversized strings from blocking the single-threaded Node.js event loop.

### 🎨 Flexible Formatting
Whether you prefer spaces or tabs, I've made the indentation customizable. You can specify any number of spaces from 0–10 or use the `-t` flag for tab-based indentation.

## Implementation and Usage

I designed the library to be universal, supporting both CommonJS (`require`) and ES Modules (`import`).

### Basic Setup
```bash
npm install json-format-validator
```

### Standard Usage
```javascript
const processAndFormatJson = require('json-format-validator');

const rawJson = '{"name":"Alice","role":"admin"}';
const result = processAndFormatJson(rawJson);

if (result.status) {
  console.log('Formatted JSON:', result.data);
}
```

### Advanced Configuration
I've allowed developers to pass custom indentation and size limits as secondary and tertiary arguments:

```javascript
// Format with 4 spaces and a 10MB size limit
const result = processAndFormatJson(largeJsonString, 4, 10);

// Format using Tab characters
const resultTabs = processAndFormatJson(input, '-t');
```

## Potential Use Cases

### 1. Express.js Middleware
I highly recommend using this as middleware to sanitize incoming raw payloads before they hit your route handlers. This ensures that your API only processes valid, safe JSON.

### 2. Git Pre-commit Hooks
You can integrate this utility into your CI/CD pipeline or Git hooks to prevent invalid JSON configuration files from ever being committed to your repository.

### 3. CLI Prettification
Because it includes a Command-Line Interface, you can quickly clean up JSON files directly from your terminal:
```bash
npx json-format config.json -t > pretty-config.json
```

## API Summary

| Parameter | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `jsonString` | string | Required | The raw JSON input to validate and format. |
| `indent` | number/string | `2` | Spacing (0–10) or `'-t'` for tabs. |
| `limitMb` | number | `5` | Max payload size in Megabytes. |