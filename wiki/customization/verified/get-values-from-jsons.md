---
title: Get Values from JSONs
description: Parse JSON files and get values from it.
published: true
date: 2023-02-10T23:03:39.271Z
tags: guide, json
editor: markdown
dateCreated: 2022-07-29T23:16:53.296Z
---

# 0. About

FancyMenu **v2.12.0+** allows you to parse JSONs via a placeholder, so you can get values from JSONs and render them as text element.

# 1. Parsing a JSON

To get content from a JSON, you will need to use the **JSON Parser** text placeholder.

> Text placeholders can be used in almost every text-based element.
To see all available text placeholders, click on the little [+] button at the right side of a text input field.
{.is-info}

## 1.1. The Placeholder

The JSON parser placeholder looks like this:
`{"placeholder":"json","values":{"source":"path_or_link_to_json","json_path":"$.some.json.path"}}`

### 1.1.1. Source
`path_or_link_to_json` is the source and needs to be replaced with a valid path or URL to a JSON file.
This can be a local path or a web URL.

### 1.1.2. JSON Path
`$.some.json.path` needs to be replaced with the path **to the value inside the JSON** you want to get (**not to confuse with the path to the JSON file**).
So you basically point to a value in the JSON to let FancyMenu know what content it should get.

> FancyMenu uses [Jayway JsonPath](https://github.com/json-path/JsonPath) to get content from JSONs.
{.is-info}

The JSON path, also known as JsonPath expression, points to the value/content of the JSON you want to get.

To learn how to write JSON paths, please take a look at the [JsonPath guide](./jsonpath)!

