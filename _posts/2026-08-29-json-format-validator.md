---
layout: post
title: "json-format-validator"
date: 2026-08-29 01:07:45 +0000
categories: projects
excerpt: "Ensuring API Stability: Introducing json-format-validator Handling JSON data is a fundamental part..."
---

# Ensuring API Stability: Introducing json-format-validator

Handling JSON data is a fundamental part of modern web development, but it comes with hidden risks. From crashing servers due to malformed syntax to security vulnerabilities like Prototype Pollution, the simple act of parsing a string can introduce significant instability. 

To solve these problems, I created **json-format-validator**, a lightweight and secure Node.js utility designed to validate, sanitize, and format JSON strings without the risk of unhandled exceptions.

[![npm version](https://img.shields.io/npm/v/json-format-validator.svg)](https://www.npmjs.com/package/json-format-validator)
[![license](https://img.shields.io/npm/l/json-format-validator.svg)](LICENSE)

## What is json-format-validator?

At its core, `json-format-validator` is a fail-safe wrapper around JSON parsing. Instead of using `JSON.parse()`—which throws a runtime error that can crash your entire process if not wrapped in a try-catch block—my utility returns a consistent status object. This ensures that your server remains online regardless of the input quality.

## Key Features

I have built this tool with a "security-first" mindset, incorporating several safeguards that standard parsing methods lack:

*   **Safe Parsing:** I've implemented custom reviver logic to strip sensitive prototype keys (`__proto__`, `constructor`) during the parsing phase. This directly prevents Prototype Pollution attacks.
*   **Fail-Safe Responses:** The utility never throws an exception. It always returns a predictable `{ status, data }` object.
*   **Payload Guard:** To protect against memory exhaustion attacks (DoS), I included a configurable size limit (defaulting to 5MB) that checks the payload size before parsing.
*   **Flexible Formatting:** You can customize the output indentation using a number (0–10 spaces) or use the `'-t'` flag for tab-based indentation.
*   **Universal Compatibility:** Whether your project uses CommonJS (`require`) or ES Modules (`import`), this utility works seamlessly.

## How to Use It

Installing the package is straightforward:

```bash
npm install json-format-validator
```

### Basic Implementation
Depending on your module system, you can integrate it as follows:

**CommonJS:**
```javascript
const processAndFormatJson = require('json-format-validator');
const rawJson = '{"name":"Alice","role":"admin"}';
const result = processAndFormatJson(rawJson);
```

**ES Modules:**
```javascript
import processAndFormatJson from 'json-format-validator';
const rawJson = '{"status":"active","count":42}';
const result = processAndFormatJson(rawJson);
```

### Advanced Customization
I have provided parameters to give you full control over how your JSON is processed:

```javascript
// Format with 4 spaces and a 10MB size limit
const result = processAndFormatJson(largeJsonString, 4, 10);

// Format using tabs
const formattedTabs = processAndFormatJson(input, '-t');
```

## Potential Use Cases

I designed this tool to be versatile, fitting into various stages of the development lifecycle:

### 1. Express.js Middleware
You can use it to sanitize and validate incoming raw payloads before they ever reach your route handlers. This ensures that your business logic only ever deals with valid, safe JSON.

### 2. Command-Line Utility
For those who prefer the terminal, I've included a CLI. You can prettify JSON files on the fly:
```bash
# Prettify a JSON file using 2 spaces
npx json-format config.json

# Prettify using tabs and save output to a new file
npx json-format data.json -t > pretty-data.json
```

### 3. Git Pre-commit Hooks
To maintain a clean codebase, you can integrate this utility into a pre-commit hook. By scanning all `.json` files in the staging area, you can prevent invalid syntax from ever being committed to your repository.

## API Summary

| Parameter | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `jsonString` | string | Required | The raw JSON input to validate and format. |
| `indent` | number/string | 2 | Indentation spaces (0–10) or `'-t'` for tabs. |
| `limitMb` | number | 5 | Max allowed payload size in Megabytes. |

**Return Value:**
An object containing `status` (boolean) indicating success, and `data` (string) containing either the formatted JSON or the original input if validation failed.