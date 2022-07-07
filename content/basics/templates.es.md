---
title: "Plantillas"
date: 2022-07-07T14:48:54+02:00
draft: true
---

## ¿Que és una plantilla?
A template is a group of files and folders agrouped inside a root folder.

## ¿Que contiene un plantilla?
Una plantilla contiene 3 tipos de elementos.

- Template specific files:
    - **owl_config.toml**
    - **.owlignore**
- Files
- Folders

### Template specific files

- #### owl_config.toml
This file is used by owl to read scripts inside this template in future versions may be used
to save some extra configuration.

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
See [here]() for more details
{{% /notice%}}

- #### .owlignore
While owl is copying files inside the root project folder may you want to avoid copy some
files from template. In this file you will save the files and folders that you don't want to copy.

**Ejemplo**
```
.git/
*.sh # glob regex
```

{{% notice note%}}
See [here]() for more details
{{% /notice%}}
