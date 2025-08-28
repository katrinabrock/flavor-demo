---
title: Setup
---

This lesson demonstrates the WIP "flavor" feature that for [carpentries workbench](https://carpentries.github.io/workbench/). Essentially, creating multiple versions of a lesson from the same episode md files.

There is a dropdown in the top right to switch between the R and python flavors of this lesson. They have slightly different content. These two versions of the site are not from forked content, but rather the content for both sites is encoded in [./episodes](https://github.com/katrinabrock/flavor-demo/tree/main/episodes) and a custom version of workbench interprets what goes where.

The feature is far from being ready for prime-time but the core functionality is there. This lesson is built with:

- [katrinabrock/sandpaper@flavor](https://github.com/katrinabrock/sandpaper/tree/flavors)
- [katrinabrock/varnish@flavor](https://github.com/katrinabrock/varnish/tree/flavors)

The `config.yaml` for this lesson has a block like this:
  
```yaml
flavors:
  r-flavor:
    title: R
    render: yes
  python-flavor:
    title: Python
    render: yes
```
