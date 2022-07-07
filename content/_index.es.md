---
title: "Inicio"
date: 2022-06-30T12:43:53+02:00
---

# Owl

[Owl](https://github.com/4strodev/owl) es una **simple** libreria que facilita la creacion de **generadores de proyecto
independientemente del lenguage de pgroamacion**.

<!--TODO add corresponding links-->
## Main features
- Basado en plantillas (locales o remotas)
- Ignora archivos con `.owlignore`
- Ejecuta comandos personalizados
- El archivo de configuracion puede ser escrito en json, yaml, toml gracias a [Viper](https://github.com/spf13/viper)

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

{{% notice info %}}
Si te gustaría aprender a hacer tus propias plantillas [mira aquí]().
{{% /notice %}}
