---
title: "Ignore files"
date: 2022-07-14T20:13:28+02:00
draft: false
weight: 20
---

Some times you don't want that owl copy a file from your template. This is where a `.owlignore` file can be useful.

## What is it?
This is a file where you declare wich files aren't going to be copied.
This tries to emulate the `.gitignore` file but it has their limitations.

## Syntax
```
# This is a comment
.git # this comment is unsuported DON'T DO THAT

# ignoring `sh` files in every subfolder of `folder`
folder/**/*.sh
```

{{<notice note>}}

Also you can include many .owlignore files in different folders of your template.

{{</notice>}}
