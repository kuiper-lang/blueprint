# Configuring Kuiper's preprocessor
Kuiper features an adaptive type checker prior to transpilation, similar to TypeScript. The type checker can be configured fully using Kuiper's **preprocessor comments** at the top of a module.

The syntax for implementing **preprocessor commands** is `-- @(directive-name)`.

| ⚙️ Tag                            | 🛠️ Functionality                                                              |
|:--------------------------------- |:-------------------------------------------------------------------------------|
|`@strict`                          | Enables full **static typing**, data must be fully annotated                   |
