# AppCompiler - Natural Language to Executable App Schema Compiler

[![HTML5](https://img.shields.io/badge/HTML5-E34F26.svg?logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-F7DF1E.svg?logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![CSS3](https://img.shields.io/badge/CSS3-Modern%20Dark-1572B6.svg?logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

A client-side domain compiler and schema synthesis engine that parses natural language software descriptions into validated, production-grade JSON architecture schemas spanning UI hierarchies, REST API endpoint definitions, and relational database schemas.

---

## Live Application

Experience the browser-based schema compiler:  
👉 **[pratapashanmukhi.github.io/appcompiler](https://pratapashanmukhi.github.io/appcompiler)**

---

## Project Overview

Modern AI-assisted software generation requires rigorous formal specifications to bridge the gap between ambiguous user prompts and deterministic source code generators. 

**AppCompiler** serves as a domain compiler pipeline for automated application scaffolding. Given high-level requirements such as:

> *"Build a SaaS invoicing platform with client management, recurring billing, PDF exports, payment tracking, and multi-currency support."*

AppCompiler analyzes user intent, tokenizes domain entities, resolves foreign key dependencies, and emits three coordinated executable schemas:
1. **UI Layout Schema**: Page routing, responsive component trees, forms, and reactive state bindings.
2. **REST API Schema**: Endpoints, HTTP verbs (`GET`, `POST`, `PUT`, `DELETE`), request/response payloads, and authentication guards.
3. **Database Schema**: Entity-relationship tables, field datatypes, constraints (`PRIMARY KEY`, `NOT NULL`, `UNIQUE`), and foreign key relationships.

### Problem Statement
- **Prompt Ambiguity**: Generative AI tools frequently emit conflicting data types or missing database relationships when prompted without structured intermediate representations.
- **Specification Drift**: Hand-written API specs, UI wireframes, and database migrations easily fall out of sync during rapid prototyping.
- **Dependency Overhead**: Many code scaffolding platforms require heavy local backend runners just to inspect structural architecture blueprints.

---

## Compiler Architecture & Pipeline

```
[ Natural Language Requirements Input ]
                   │
                   ▼
  [ Stage 1: Lexical & Entity Extraction ]
   ├── Entity Disambiguation (Users, Projects, Billing)
   ├── Auth & RBAC Scope Identification (Admin, Sales, Viewer)
   └── Third-Party Integration Flags (Stripe, S3, Email)
                   │
                   ▼
  [ Stage 2: Structural Schema Synthesis ]
   ├── Relational Table Modeling & Foreign Key Cardinality
   ├── RESTful Endpoint Generation & HTTP Verb Mapping
   └── UI View Tree Composition & Navigation Routing
                   │
                   ▼
  [ Stage 3: Verification & Compilation ]
   ├── Schema Consistency & Constraint Validation
   └── Deterministic Executable JSON Bundling (UI, API, DB)
                   │
                   ▼
  [ Interactive In-Browser Studio Output ]
   └── Live Search, JSON Inspector, and Exportable Manifest
```

---

## Key Features

- **Multi-Stage Semantic Synthesis**: Translates unstructured functional requirements into structured architectural specifications.
- **Triple-Layer Specification**: Emits complete UI, API, and Database manifests in a unified compilation run.
- **Zero-Dependency Portability**: Implemented purely with standards-compliant HTML5, CSS3, and modern JavaScript, running 100% client-side with zero external build tools.
- **Interactive Schema Visualizer**: Features live syntax-highlighted JSON rendering, copy-to-clipboard actions, and quick preset templates (CRM, SaaS Invoicing, Trello clone).

---

## Project Structure

```
appcompiler/
├── index.html          # Self-contained compiler engine, styles, and UI studio
├── .gitignore          # Editor and OS file exclusions
└── README.md           # Comprehensive technical documentation
```

---

## Getting Started

### Prerequisites

- Any modern web browser (Chrome, Edge, Firefox, Safari)

### Local Usage

1. **Clone the repository:**
   ```bash
   git clone https://github.com/pratapashanmukhi/appcompiler.git
   cd appcompiler
   ```

2. **Launch directly in your browser:**
   - Double-click `index.html` to open in your default browser.
   - Or serve locally:
     ```bash
     npx serve .
     # or python -m http.server 8000
     ```

---

## Author

**Shanmukhi Pratapa**  
B.Tech Computer Science & Engineering (Artificial Intelligence & Machine Learning)  
VIT-AP University  
GitHub: [@pratapashanmukhi](https://github.com/pratapashanmukhi)
