---
title: "Home page"
date: 2022-06-30T12:43:53+02:00
---

# Owl a simple project creator library

[Owl](https://github.com/4strodev/owl) is a **simple** library that helps you to make **project creators**,
the programing **language or framework doesn't matter**.

<!--TODO add corresponding links-->
## Main features
- Template based (local or remote templates)
- Ignore files with `.owlignore`
- Execute custom commands
- Config file can be writed in json, yaml, toml thanks to [Viper](https://github.com/spf13/viper)

## Example
```go
package main

import (
	"flag"
	"fmt"
	"os"
	"path"

	"github.com/4strodev/owl"
	"github.com/4strodev/owl/template"
)

var (
	projectName     string
	moduleName      string
	projectTemplate string
	verboseOutput   bool
)

func main() {
	flag.StringVar(&projectName, "name", "my-app", "-name <project name>")
	flag.StringVar(&projectTemplate, "template", "go-cli", "-template <project template>")
	flag.StringVar(&moduleName, "module", "", "-template <project template>")
	flag.BoolVar(&verboseOutput, "verbose", false, "-verbose")
	flag.Parse()

	if moduleName == "" {
		fmt.Printf("Set go module name: ")
		fmt.Scanln(&moduleName)
	}

	project := owl.NewProject(
		owl.ProjectConfig{
			Name:         projectName,
			TemplateName: projectTemplate,
			LocalTemplatesDirs: []string{
				path.Join(os.Getenv("HOME"), "Templates"),
			},
			VerboseOutput: verboseOutput,
		}, template.TemplateConfig{
			ConfigType: "toml",
			Context: map[string]any{
				"ModuleName": moduleName,
			},
		},
	)

	err := project.Create()
	if err != nil {
		switch err.Error() {
		case owl.DIR_EXISTS:
			fmt.Printf("Folder %s already exists\n", projectName)
			break
		case owl.TEMPLATE_NOT_FOUND:
			fmt.Printf("Template '%s' not found\n", project.Config.TemplateName)
			break
		default:
			fmt.Printf("Error creating project: %s\n", err)
			break
		}
		os.Exit(1)
	}
}
```

    go run .

{{% notice info %}}
If you would like to know how to make your custom templates [see here]( {{.Page.Site.BaseURL}} ).
{{% /notice %}}
