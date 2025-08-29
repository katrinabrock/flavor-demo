# Flavor Proof of Concept

## About

This repo contains a sample lesson that demonstrates the "flavor" feature that could be added to carpentries workbench. Essentially, creating multiple versions of a lesson from the same episode md files. You can see:

- https://katrinabrock.github.io/flavor-demo/r-flavor/
- https://katrinabrock.github.io/flavor-demo/python-flavor/

There is a dropdown in the top right to switch between them. They have slightly differen content. These two versions of the site are not from forked content, but rather the content for both sites is encoded in [./episodes](./episodes) and a custom version of workbench interprets what goes where.

The feature is far from being ready for prime-time but the core functionality is there. This lesson is built with:

- [katrinabrock/sandpaper@flavor](https://github.com/katrinabrock/sandpaper/tree/flavors)
- [katrinabrock/varnish@flavor](https://github.com/katrinabrock/varnish/tree/flavors)

## Lesson-author facing spec

Flavors must be configured in config.yaml:

```yaml
flavors:
  - <flavor id>:
    title: <User-facing name>
    render: FALSE
```

flavor id (key) and `title` are required. `render` is optional and defaults to `TRUE`

Example:

```yaml
flavors:
  - vanilla:
    title: "Vanilla"
    render: FALSE
  - chocolate;
    title: "Chocolate"
  - strawberry:
    title: "Strawberry"
  - blueberry:
    title: "Blueberry"
  - cookiesncream:
    title: "Cookies 'N' Cream"
```

### Within-episode flavored content

In the episodes, by default content is included in every flavor. To make content within an episode vary by flavor, put it inside a `flavored` block. Inside the `flavored` block, there should be a block for each flavor.

Example:

```markdown
## Ingredients

- Milk
- Sugar
- Cream
- Ice
::::::::::::::::::::::::::::::::::::::::::::::::::::::: flavored
:::::::::::::::::::::::::: vanilla 
- Vanilla Extract
:::::::::::::::::::::::::::::::::::
:::::::::::::::::::::::::: chocolate
- Chocolate Powder
::::::::::::::::::::::::::::::::::::
:::::::::::::::::::::::::: strawberry
- Fresh Strawberries
:::::::::::::::::::::::::::::::::::::
:::::::::::::::::::::::::: strawberry
- Fresh Blueberries
:::::::::::::::::::::::::::::::::::::
:::::::::::::::::::::::::: cookiesncream
- "Sandwich" cookies
::::::::::::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
```

Will result in each flavor only showing its corresponding final ingredient.

## Full episode specific to some flavors

You can also write an entire episode that only appears in some flavors by adding the `flavors` key to the top yaml with the flavor ids of the flavors it should be included in.


```yaml
---
title: "Prepping the Fruit"
flavors: [strawberry, blueberry] 
---

Start by washing the fruit...
```

## DONE

These parts are already built:
- Core functionality of within-episode differences accross flavors.
- Core functionality of flavor-specific episodes
- Sidebar
  - Looks correct on episode pages
  - Redirects correctly
- Header looks correct and redirects correctly
- Dropdown is present and works

Only tested with the config in this repo. You are welcome to test with your own config, but be warned there is a high chance it will error without giving you a helpful message as to why.

## TODO

### Known Bugs

- Need to add overall landing page and 404. Currently there is only a landing page/404 for each flavor.
- Next episode and previous episode links don't work
- Extraneous commas in non-episode sidebar (e.g. CoC, Instructor Notes etc.)
- "Key Points", "Extract All Images", "All in One" sidebar is very broken
- Switching flavors on a flavor-specific episode to a flavor that doesn't have it results in github 404. Should result in either custom 404 or better still redirect to previous/next page on target flavor.

### Known Must-do Tasks

- DRY up code. Especially:
  - Move "flavors_to_build" logic to one place.
  - move select_flavor_data from build_html into getter section
  - generally move more of the flavor-specific logic into setters and getters and less repeating in each function that needs them.
- Update pegboard
  - add flavor logic to config checker (if there is such a thing)
    - valid ids and names
    - at least one flavor configured to build
  - add flavor logic to top yaml checker
    - `flavors` only set in episodes if `flavors` set in config
  - add flavor logic to div checker
    - only configured flavors inside a flavored block
    - nothing inside the flavor block but outside a particular flavor
    - every configured flavor (or at least those configured to render) are inside 
- Test more cases
  - more than two flavors
  - mix of render and not render
  - exactly one flavor to render
  - defaulting to render
  - Rmd instead of md
  - test flavored objective, questions etc.
- Build test suite to test this functionality
- Regression testing - Make sure we didn't break anything that was working before. If these area already included in test, all we need to do is get that test to pass. If not included in a test, test should be written.
  - simple test with no flavors (I made an attempt not to break things, but didn't actually verify if I succeeded. Probably I didn't.)
  - translated site
  - test that setting episode order still works

### Possible Spec Changes

- switch to british spelling for consistency with other terms?
- rename render=FALSE to hide=TRUE?
- have an option in config to render a flavor, but hide it from the dropdown (so as not to confuse learners)

### Documentation

- "how to add flavors to a lesson" doc
- "working with flavored lessons" doc
