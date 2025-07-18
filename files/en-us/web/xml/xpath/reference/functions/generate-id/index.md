---
title: generate-id
slug: Web/XML/XPath/Reference/Functions/generate-id
page-type: xpath-function
sidebar: xmlsidebar
---

The `generate-id` function generates a unique id for the first node in a given node-set and returns a string containing that id.

## Syntax

```plain
generate-id( [node-set] )
```

### Parameters

- `node-set` (optional)
  - : An id will be generated for the first node in this node-set. If omitted, the current context node will be used.

### Return value

A string containing the generated id.

## Description

- The same id must be generated every time for the same node in the current document in the current transformation.
- The generated id may not be the same in subsequent transformations.

This function is an XSLT-specific addition to XPath. It is not a part of the core XPath function library.

## Specifications

[XSLT 1.0 12.4](https://www.w3.org/TR/xslt-10/#function-generate-id)

## Gecko support

Supported.
