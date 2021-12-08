---
categories: ["Examples", "Placeholders"]
tags: ["test","docs"] 
title: "Getting Started"
linkTitle: "Getting Started"
weight: 2
description: >
  What does your user need to know to try your project?
---

{{% pageinfo %}}
This is a placeholder page that shows you how to use this template site.
{{% /pageinfo %}}

Information in this section helps your user try your project themselves.

* What do your users need to do to start using your project? This could include downloading/installation instructions, including any prerequisites or system requirements.

* Introductory “Hello World” example, if appropriate. More complex tutorials should live in the Tutorials section.

Consider using the headings below for your getting started page. You can delete any that are not applicable to your project.

## Prerequisites

The prerequisites are:

- [Nim language](https://nim-lang.org/install.html)
- Open Cascade library: for instance, in ArchLinux, you can just do: `$ yay -S opencascade`. Check in your own distribution.

{{< alert color="warning" title="Warning" >}}Windows is untested yet.{{< /alert >}}

## Installation

It can be installed using nimble:

```
$ nimble install https://github.com/mantielero/occt.nim
```


## Try it out!

Once installed, you can run your first example. For example, in order to create a point, you could create the text file `ex00.nim`:

```nim
include occt
let aPnt1 = newPnt( 20, 30, 40)
echo aPnt1
```

This code can be compiled and run with:
```bash
$ nim cpp ex00
```
