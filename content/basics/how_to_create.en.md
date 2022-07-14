---
title: "How to create a template"
date: 2022-07-08T16:18:11+02:00
draft: false
weight: 30
---

To create a template you need a public git repository and a text editor.

{{% notice info %}}
This example is goint to be an application with go and fiber.
{{% /notice %}}

## Setup
First we gonna create a folder (this folder will be where template files are going to reside).
    
    mkdir go-fiber

Subsequently we initialize our git repo.

    cd go-fiber
    git init

## Inital files
We gona create the inital files. This havo the be files that we know that don't need to be loaded dynamically.
In future versions you will can use variables inside your inital files.

`main.go`
```go
package main

import (
    "log"

    "github.com/gofiber/fiber/v2"
)

func main() {
    app := fiber.New()

    app.Get("/", func (c *fiber.Ctx) error {
        return c.SendString("Hello, World!")
    })

    log.Fatal(app.Listen(":3000"))
}
```

`.editorconfig`
```.editorconfig
root = true

[*]
charset = utf-8
end_of_line = lf
insert_final_newline = true

[*.go]
indent_size = 8
indent_style = tab

[*.md]
indent_size = 4
indent_style = space
```

## Configuration files
The `owl_config.toml` fil accpets variables that we send with a `map` to owl to can use it in our configuration files.

`owl_config.toml`

```toml
[scripts.oncreate.universal]
git_init = ["git init"]

[scripts.onmount.universal]
init_module = ["go mod init {{ .ModuleName }}", "go get github.com/gofiber/fiber/v2"]
```

`.owlignore`

```
.git
README.md
```

## Push to github
Then you can push to a github repo and use this template with their url.
