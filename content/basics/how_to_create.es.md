---
title: "Como crear una plantilla"
date: 2022-07-08T16:18:13+02:00
draft: false
weight: 3
---

Para crear una plantilla necesitas tener un repositorio de git publico y un editor de texto.

{{% notice info %}}
Este ejemplo se ara con una aplicacion con go y fiber
{{% /notice %}}

## Preparativos
Primero crearemos una carpeta (esta carpeta sera donde estaran los archivos de nuestra plantilla).
    
    mkdir go-fiber

Posteriormente inicializaremos nuestro repositorio.

    cd go-fiber
    git init

## Archivos iniciales
Vamos a crear los archivos inizales. Estos tienen que ser archivos que sabemos que no
necesitan ser cargados de manera dinámica. En futuras versiones se implementará la funcionalidad de añadir
variables a los archivos de tu plantilla. Opcionalmente puedes crear un archivo README.md.

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
```
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

## Archivos de configuración
El archivo `owl_config.toml` admite variables que mandaremos con un `map` a owl para poder usarlos en nuestros archivos
de configuración.

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
