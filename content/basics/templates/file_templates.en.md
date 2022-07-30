---
title: "File templates"
date: 2022-07-30T13:59:20+02:00
draft: false
weight: 30
---

Also you can create files that will be parsed as go text templates.

## How to make it?
To do that you only need to create a file with the result name like **main.go** with the `.tmpl` extension.

{{% notice info %}}
The variables depends on how to project generator was programmed.
{{% /notice %}}

For the example I will use [raven-fiber-template](https://github.com/4strodev/raven-fiber-template) **main.go.tmpl** file.

```go
package main

import (
    "log"
    "{{ .ModuleName }}/internal/server"
)

func main() {
    log.Fatal(server.App.Listen(":3000"))
}
```

{{% notice info %}}
For more information about text templates visit [go text templates](https://pkg.go.dev/text/template).
{{% /notice %}}
