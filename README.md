# Grupo 6 – Ingsis

Welcome to the Grupo 6 organization! This organization hosts two main projects: **Printscript**, a custom programming language, and **Snippet Searcher**, a microservices application built on top of it.

---

## Printscript

Printscript is a custom programming language developed from scratch. It is structured around the following components:

- **Lexer** – tokenizes the source code into a stream of tokens.
- **Parser** – builds an Abstract Syntax Tree (AST) from the token stream.
- **Interpreter** – executes the AST to produce program output.
- **Formatter** – applies configurable style rules to source code.
- **Linter** – enforces coding conventions and detects potential issues.
- **CLI** – command-line interface to run, format, and lint Printscript programs.

Design patterns such as **Factory** are used throughout the codebase to keep the components extensible and decoupled.

Printscript supports two versions of the language specification:
- **Version 1.0** – the initial language release.
- **Version 1.1** – an extended version with additional features.

---

## Snippet Searcher

Snippet Searcher is a web application that lets users store, share, and run code snippets written in Printscript. The backend is composed of three microservices:

### Service (Manager)
The central microservice that receives and orchestrates all incoming requests. It coordinates communication between the other services and manages the asynchronous event flow with the Engine.

### Engine
Responsible for processing code snippets. Given a snippet, it:
- **Validates** whether the code is syntactically and semantically correct (using the Printscript lexer/parser/linter).
- **Runs** the snippet and returns the execution result (using the Printscript interpreter).

### Authorization
Manages access control for snippets. It determines whether a user can:
- **Edit** a snippet (owner).
- **View** a snippet (shared access).
- **Have no access** to a snippet.

User identity is provided by **Auth0** for authentication. The Authorization service stores and checks user IDs to enforce the appropriate permissions.

---

## Infrastructure & Tech Stack

| Concern | Technology |
|---|---|
| Backend language | Kotlin |
| Frontend language | TypeScript |
| End-to-end testing | Cypress |
| Async event bus | Redis |
| Snippet storage | Azurite (Azure Blob Storage emulator) |
| Reverse proxy / TLS | Nginx + Let's Encrypt (HTTPS) |
| Authentication | Auth0 |