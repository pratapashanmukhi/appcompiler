# AppCompiler — Natural Language to Executable App Schema Compiler

[![HTML5](https://img.shields.io/badge/HTML5-E34F26.svg?logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E.svg?logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

A multi-stage compiler pipeline interface that converts plain English software requirements into validated, executable JSON configurations across UI schemas, REST API endpoints, and relational database schemas.

---

## Live Prototype

Try the compiler interface online:  
**[pratapashanmukhi.github.io/appcompiler](https://pratapashanmukhi.github.io/appcompiler)**

---

## What It Does

AppCompiler functions as a **domain compiler for automated software generation**. It takes a natural language specification such as:

> *"Build a CRM with authentication, contacts table, role-based access control (admin, sales, viewer), Stripe billing integration, and an analytics dashboard."*

...and synthesizes a complete, validated architectural JSON configuration encompassing:
- **UI Schema**: Pages, view components, reactive form bindings, and responsive layout hierarchy.
- **API Schema**: REST routes, HTTP verbs, auth scopes, headers, request bodies, and expected status codes.
- **Database Schema**: Relational entity tables, foreign keys, cardinality relationships, and index definitions.

---

## Key Features

- **Multi-Stage Compiler Pipeline**: Lexical tokenization of intent, entity extraction, structural validation, and syntax tree compilation.
- **Interactive Schema Visualizer**: In-browser preview rendering interactive JSON trees and live schema previews.
- **Zero-Dependency Architecture**: Standalone, portable client-side single-page application requiring no backend runtime to explore.
- **Exportable Manifests**: Download compiled JSON specifications ready for downstream code generation harnesses.

---

## Project Structure

```
appcompiler/
├── index.html          # Interactive compiler interface & visualization engine
├── .gitignore          # Environment & editor exclusions
└── README.md           # Documentation
```

---

## Getting Started

1. **Clone the repository:**
   ```bash
   git clone https://github.com/pratapashanmukhi/appcompiler.git
   cd appcompiler
   ```

2. **Open the application:**
   Open `index.html` in your web browser, or serve with:
   ```bash
   npx serve .
   ```

---

## Author

**Shanmukhi Pratapa**  
B.Tech CSE (AI & ML) — VIT-AP University  
GitHub: [@pratapashanmukhi](https://github.com/pratapashanmukhi)
