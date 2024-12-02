---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
draft: true
description: ""
tags: ["project"]
thumb: true
params:
    author: "Nykenik24" 
---

{{< lead >}}
{{ .Name }}
{{< /lead >}}
