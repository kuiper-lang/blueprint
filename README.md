# 📑 Luz - Language Specification
### Description
This document details the key philosophy and rationale behind designing Luz, a general-purpose scripting language constructed as a dialect on top of Lua, a lightweight embeddable scripting language.

### Key Motivation
The motivation behind developing Luz as a distinct superset of Lua is derived from its minimal syntax, as well as the emphasis on reflective and metaprogramming features, making it incredibly flexible and expressive.

This specification will outline how Lua, a fast, minimal, embeddable scripting language, will be adapted into Luz, an expressive general-purpose dialect that maintains Lua's speed and minimalism while introducing several modern features, such as native support for async/await, gradual typing, error handling, match statements, and pipelining.

### Why Luz?
- Luz bridges the gap between Lua and modern languages, such as TypeScript, Rust, and Elixir while preserving Lua's clean and readable syntax. This is achieved through resolving key pain points with general-purpose programming in Lua, which is typically optimised to embedding within existing applications.

- Versus Lua, existing scripting languages such as Python, JavaScript, and Ruby sacrifice speed and runtime minimalism via larger runtime dependencies and performance overhead through abstraction. This is circumvented by Luz's key philosophy to maintain Lua's lightweight embeddability while evolving its syntax with new modern features which ease developer grievances.