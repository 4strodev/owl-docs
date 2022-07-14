---
title: "Scripts"
date: 2022-07-12T16:23:11+02:00
draft: false
weight: 10
---

A script is a sequence of commands that owl will execute during the creation of a project.

## How to declare scripts?
In your config file you will declare two sections. `oncreate` and `onmount` these are the
two main moments when scripts are executed.

Then inside each of this sections there are 4 types of scripts:

- universal scripts

    This scripts are executed on **all** operating systems.

- linux scripts

    This scripts are executed only in **linux**.

- macos scripts

    This scripts are executed only in **macos**.

- windows scripts

    This scripts are executed only in **windows**.

## Example

{{< tabs groupid="config">}}
{{% tab name="toml" %}}
```toml
# golang template example configuration

# Possible options universal, linux, windows, macos
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
  # Possible options universal, linux, windows, macos
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

// Possible options universal, linux, windows, macos
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

{{< notice warning >}}
Before owl execute a script. Changes the working directory to the template's root folder.
{{< /notice >}}
