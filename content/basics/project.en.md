---
title: "Project"
date: 2022-07-09T11:27:15+02:00
draft: true
weight: 1
---

This is easy to understand. A project is the result of a template with a configuration applied.
When you create a project you have to pass a `ProjectConfig` struct and a `TemplateConfig` struct.

```go
package main

import (
    "github.com/4strodev/owl"
)

func main() {
    // Initalizing your project
    project := owl.NewProject(
        // You have to pass the project config which saves information like:
        // - The project name
        // - The template that the project will use it can be an url to a git repository
        // - Where to find this template locally
        owl.ProjectConfig{
            Name:         "my-project",
            TemplateName: "project-template",
            LocalTemplatesDirs: []string{
                path.Join(os.Getenv("HOME"), "Templates"),
            },
            VerboseOutput: false,
        
        // Here you will save:
        // - Which type of config file you will use
        // - The variables that you want to pass to your config
        }, template.TemplateConfig{
            ConfigType: "toml",
            Context: map[string]any{
                "ModuleName": moduleName,
            },
        },
    )
}
```

{{% notice info %}}
In `LocalTemplatesDirs` we are using `os.Getenv` because we have to parse environemnt variables outiste the path.
{{% /notice %}}
