---
title: "Git - GitHub Workflow"
date: 2021-10-21T10:29:17+02:00
linkTitle: "Git Workflow"
weight: 3
description: >
  Utilidades git y github
docs: >
  https://www.freecodecamp.org/news/how-to-fork-a-github-repository/
  https://desarrolloweb.com/articulos/fork-git
  https://docs.github.com/es/get-started/quickstart/fork-a-repo
  https://gist.github.com/james-priest/74188772ef2a6f8d7132d0b9dc065f9c

draft: false

---

{{% pageinfo %}}
**{{< emoji ":books:" >}} Documentación**:
* https://docs.github.com/es/get-started/quickstart/fork-a-repo {{< emoji ":heartpulse:" >}} 
* https://docs.github.com/es/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork
* https://www.atlassian.com/git/tutorials/comparing-workflows/forking-workflow
{{% /pageinfo %}}



![Fork-Pull request](https://www.freecodecamp.org/news/content/images/2022/02/GitHub-Fork.gif)
Fuente imagen: https://www.freecodecamp.org/news/how-to-fork-a-github-repository/


## Fork de un repositorio

Interfaz de github

## Clonar repositorio 

```bash    
$ git clone <url de mi repositorio>
```
## Configurar remoto upstream

```bash    

$ git remote -v
> origin  <url> (fetch)
> origin  <url> (push)

$ git remote add upstream <repositorio original>
$ git remote -v
```
## Creación de ramas / commits

## Sincronizar con original

```bash
$ git fetch upstream
```
* {{< emoji ":closed_book:" >}}  https://www.atlassian.com/git/tutorials/git-forks-and-upstreams
  
## Pull request