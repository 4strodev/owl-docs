---
title: "Plantillas"
date: 2022-07-07T14:48:54+02:00
draft: false
---

## ¿Que és una plantilla?
Una plantilla es un grupo de archivos i carpetas agrupados en una carpeta raíz.

## ¿Que contiene un plantilla?
Una plantilla contiene 3 tipos de elementos.

- Archivos especificos de la plantilla:
    - **owl_config.toml**
    - **.owlignore**
- Archivos
- Carpetas

### Archivos especificos de la plantilla

- #### owl_config.toml
Este archivo lo usa owl para leer los scripts dentro de la plantilla,
en el futuro puede que se use para guardar mas información. Puede ser
tanto un archivo: **toml, yaml y json**

**Ejemplo**
{{< tabs groupId="config" >}}
{{% tab name="toml" %}}
```toml
# golang template example configuration
[scripts.oncreate.universal]
init_git = ["git init"]

[scripts.onmount.universal]
init_package = [
    "go mod init {{ .ModuleName }}",
    "go mod tidy"
]
```
{{% /tab %}}
{{% tab name="yaml" %}}
```yaml
# golang template example configuration
scripts:
  oncreate:
    universal:
      init_git: ["git init"]
  onmount:
    universal:
      init_package:
        - "go mod init {{ .ModuleName }}"
        - "go mod tidy"
```
{{% /tab %}}
{{% tab name="json" %}}
```json
// golang template example configuration
{
    "scripts": {
        "oncreate": {
            "universal": {
                "init_git": ["git init"]
            }
        },
        "oncreate": {
            "universal": {
                "init_package": [
                    "go mod init {{ .ModuleName }}",
                    "go mod tidy"
                ]
            }
        },
    }
}
```
{{% /tab %}}
{{< /tabs >}}

{{% notice note%}}
Consulte [aquí]() para mas detalles
{{% /notice%}}

- #### .owlignore
Mientras owl copia archivos dentro de la carpeta de proyecto quizas querras evitar copiar
algunos archivos de la plantilla. En este archivos estaran los archivos y carpetas que no quieres copiar.

**Ejemplo**
```
.git/
*.sh # glob regex
```

{{% notice note%}}
Consulte [aquí]() para mas detalles
{{% /notice%}}
