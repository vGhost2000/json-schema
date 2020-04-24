---
layout: project
version: 1.x
title: Boolean type
description: php opis json schema validation of boolean type
keywords: opis, php, json, schema, boolean
---

The `boolean` type is used to validate boolean values (`true` or `false`).

{% capture schema %}
```json
{
  "type": "boolean"
}
```
{% endcapture %}
{% capture data %}
|Input|Status|
|-----|------|
| `true`{:.language-json} | *valid*{:.text-success.text-normal} |
| `false`{:.language-json} | *valid*{:.text-success.text-normal} |
| `"true"`{:.language-json} | *invalid*{:.text-danger.text-normal} - is string |
| `null`{:.language-json} | *invalid*{:.text-danger.text-normal} - is null|
| `0`{:.language-json} | *invalid*{:.text-danger.text-normal} - is integer/number|
{:.table}
{% endcapture %}
{% include tabs.html 1="Schema" 2="Data" _1=schema _2=data %}

## Validation keywords

The `boolean` type has no specific validation keywords.
