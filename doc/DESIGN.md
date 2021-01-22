<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [IDeal high level design](#ideal-high-level-design)
    - [Modularization](#modularization)
    - [Usage Models](#usage-models)
    - [Configuration by convention](#configuration-by-convention)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# IDeal high level design

## Design principals

On top of [Tenets](https://github.com/oantoshchenko/IDeal/blob/main/README.md#tenets), IDeal's design is driven by 
some key principal. Should Tenet and Design Principal compete, Tenet always takes president.

### Modularization

IDeal is built as a set of libraries that is bind together to two types of executables (web service and local demon).

### Usage Models

IDeal can be used in 3 different modes:

1. As a web service.
1. As a local demon.
1. As a Rust library.

### Configuration by convention

We follow a principal of configuration by convention (see **Convenient** in
[Tenets](https://github.com/oantoshchenko/IDeal/blob/main/README.md#tenets) section). In practice it means that when you
first start working with IDeal, given you made a choice how you will run it (see [Usage Models](#usage-models) section),
IDeal will run with "sensible" defaults. The goal here is to create as little traction for the user as possible.
Configuration can be changed but IDeal should not require any configuration to run (besides selecting
a [Usage Model](#usage-models)).

## Architecture

**NOTE:** you will need [Github + Mermaid](https://github.com/BackMarket/github-mermaid-extension) to see rendered 
diagrams.

```mermaid

```