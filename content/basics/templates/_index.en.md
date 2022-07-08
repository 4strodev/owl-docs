---
title: "Templates"
date: 2022-07-07T14:21:05+02:00
draft: false
---

## What is a template?
A template is a group of files and folders agrouped inside a root folder.

## What a template contains?
A template contains 3 types of elements.

- Template specific files:
    - **owl_config.toml**
    - **.owlignore**
- Files
- Folders

### Template specific files

- #### owl_config.toml
This file is used by owl to read scripts inside this template in future versions may be used
to save some extra configuration. It can be a: **toml, yaml and json**.

**Example**
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
While owl is copying files inside the project folder may you want to avoid copy some
files from template. In this file you will save the files and folders that you don't want to copy.

**Example**
```
.git/
*.sh # glob regex
```

{{% notice note%}}
See [here]() for more details
{{% /notice%}}
