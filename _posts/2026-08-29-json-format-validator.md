---
layout: post
title: "json-format-validator"
date: 2026-08-29 01:07:45 +0000
categories: projects
excerpt: "Building Resilient Applications with json-format-validator When building Node.js applications, hand..."
---

# Building Resilient Applications with json-format-validator

When building Node.js applications, handling JSON input is a daily necessity. However, relying solely on `JSON.parse()` can be risky. A single malformed string can throw a runtime exception that crashes your entire server, and unchecked payloads can open the door to security vulnerabilities like Prototype Pollution or memory exhaustion.

To solve these challenges, I created **json-format-validator**, a lightweight, secure utility designed to validate, sanitize, and format JSON strings without the risk of unhandled exceptions.

![npm version](https://img.shields.io/npm/v/json-format-validator.svg) ![license](https://img.shields.io/npm/l/json-format-validator.svg)

## What is json-format-validator?

At its core, `json-format-validator` is a fail-safe wrapper for JSON processing. Instead of throwing errors that require bulky try-catch blocks across your codebase, it returns a consistent status object. This ensures that your application remains stable regardless of the quality of the input it receives.

## Key Features

### 🛡️ Security-First Parsing
Security is baked into the parsing logic. I have implemented safeguards against two common attack vectors:
*   **Prototype Pollution Defense:** The utility uses custom reviver logic during parsing to strip sensitive keys like `__proto__` and `constructor`, neutralizing object prototype injection attempts.
*   **Payload Guard:** To prevent memory exhaustion attacks (DoS), the tool enforces a configurable string size limit (defaulting to 5MB), ensuring the Node.js event loop isn't blocked by oversized payloads.

### ⚡ Fail-Safe Responses
I designed the tool to be "crash-proof." If the input is not a string, contains invalid syntax, or exceeds the size limit, the utility doesn't crash. Instead, it returns:
`{ status: false, data: [original_input] }`

On success, it returns:
`{ status: true, data: [formatted_json_string] }`

### 🎨 Flexible Formatting
Formatting is highly customizable to fit your project's style guide:
*   **Space Padding:** Supports customizable indentation from 0 to 10 spaces.
*   **Tab Support:** Use the `'-t'` flag to format with tab characters.

### 📦 Universal Compatibility
Whether you are working on a legacy project or a modern stack, I've ensured the library works seamlessly with both **CommonJS (`require`)** and **ES Modules (`import`)**.

## Potential Use Cases

### 1. Express.js Middleware
One of the most effective ways to use this utility is as a middleware layer. I can validate and sanitize raw payloads before they ever reach the route handlers, ensuring that only clean, valid JSON is processed by the business logic.

### 2. Git Pre-commit Hooks
To maintain a clean codebase, I use this utility in pre-commit hooks. By scanning all staged `.json` files, I can prevent invalid JSON syntax from ever being committed to the repository.

### 3. CLI Tooling
The project includes a Command-Line Interface (CLI), making it easy to prettify configuration files or data dumps directly from the terminal:
```bash
npx json-format config.json -t > pretty-config.json
```

## Quick Integration Guide

Installing the package is straightforward:
```bash
npm install json-format-validator
```

Here is a basic example of how I implement it in a script:

```javascript
const processAndFormatJson = require('json-format-validator');

const rawJson = '{"name":"Alice","role":"admin"}';
const result = processAndFormatJson(rawJson, 4, 10); // 4 spaces, 10MB limit

if (result.status) {
    console.log('Formatted JSON:', result.data);
} else {
    console.error('Invalid JSON provided.');
}
```

## API Reference

| Parameter | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `jsonString` | string | **Required** | Raw JSON string to validate and format. |
| `indent` | number \| string | `2` | Indentation spaces (0–10) or `'-t'` for tabs. |
| `limitMb` | number | `5` | Maximum allowed payload size in Megabytes. |