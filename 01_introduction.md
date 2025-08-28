---
title: "Flavoring Within an Episode"
teaching: 10 # teaching time in minutes
exercises: 2 # exercise time in minutes
---


## Example Flavored Block

:::::::::::::::::::::::::::::::::::: flavored

::::::::::::::::: r-flavor

Here's some R code:

```r
paste("This", "new", "lesson", "looks", "good")
```

:::::::::::::::::::::::::::

::::::::::::::::: python-flavor

Here's some python code:

```python
' '.join(['This', 'new', 'lesson', 'looks', 'good'])
```

::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::

You should only see either python or R code above, not both, even though both appear in the markdown.

## How it looks in Markdown

A flavored block looks like this in Markdown:

````markdown
:::::::::::::::::::::::::::::::::::: flavored

::::::::::::::::: r-flavor

Here's some R code:

```r
paste("This", "new", "lesson", "looks", "good")
```

:::::::::::::::::::::::::::

::::::::::::::::: python-flavor

Here's some python code:

```python
' '.join(['This', 'new', 'lesson', 'looks', 'good'])
```

::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::
````