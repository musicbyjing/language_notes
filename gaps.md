# HTML5

## Basics

- Opening declaration: `<!DOCTYPE html>`
    - Then `<html lang="en-US">`
- Character encoding declaration (inside `<head>`): `<meta charset="UTF-8">` 
- Set default viewport to device screen width: `<meta name="viewport" content="width=device-width, initial-scale=1.0">`

## Semantic elements

![Semantic element graphic](https://s3.amazonaws.com/viking_education/web_development/web_app_eng/html5_sectioning_high_level.jpg)

Element | Description | Notes
---| ---|---|
`<section>` | section in a document | 
`<article>` | independent, self-contained content | e.g. forum, blog post, news story <br> *no specific rules to nest `<section>`, `<article>` and `<div>`*
`<header>` | document or section header
`<footer>` | document or section footer | e.g. copyright, author
`<nav>` | major block of navigation links | e.g. navbar
`<aside>` | sidebar content
`<figure>` and `<figcaption>` | `<figure>` wraps an `<img>` and a `<figcaption>`

# CSS

## `position` attribute

- Not inherited
- Default value is *static*

Attributes:
| <!-- --> | <!-- -->
---|---
*static* | elements render in order as they appear in the document
*absolute* | element positioned relative to its first positioned (non-static) ancestor element
*fixed* | element positioned relative to browser window, i.e. scrolling won't move it
*relative* | element positioned relative to its normal position
*sticky* | element positioned based on user's scroll position; toggles from *relative* to *fixed* once you scroll past a certain point
(*initial* | sets property to its default value)
(*inherit* | inherits property from its parent element)

- `z-index` property is like "bring to front" or "send to back"; higher stack orders are in front

## Box model

![CSS Box model](https://cdn-images-1.medium.com/max/565/1*6DrszcyPybYDGziiS9CWdg.png) 
- `margin` and `padding` are transparent
- `outline` is drawn outside `border`
- Setting `width` and `height` of an element just sets the width and height of the **content area**; must add padding, borders, margins for full size of element

## Flexbox

- Negates need for float or positioning
- **Parent container** defined using `display: flex`

Properties:
| <!-- --> | <!-- --> |  <!-- -->
---|---|---
`flex-direction` | direction in which the container stacks the flex items | *column, column-reverse, row, etc.*
`flex-wrap` | whether flex items should wrap or not | *wrap, nowrap, wrap-reverse*
`flex-flow` | shorthand for both above properties
`justify-content` | aligns flex items horizontally | *center, flex-start, flex-end, space-around, space-between*
`align-items` | align flex items vertically | as above, but *baseline* aligns by text baselines
`align-content` | align baselines

- Child elements of a flex container automatically become flex items

## Flexbox vs CSS Grid

- Flexbox is a largely **one-dimensional** solution (doesn't care about columns)
- Flexbox is **content-first** while CSS Grid is **layout-first**

## CSS Grid

- Set `display` to *grid* or *inline-grid* to make an element a **grid container**
    - Direct children of the container become **grid items**
- **gaps**: space between each column/row; can be adjusted with `grid-column-gap`, `grid-gap`, etc.
- **lines**: lines between each row/column
    ```
    .item1 {
        grid-column-start: 1;
        grid-column-end: 3;
    }
    ```
    - This makes the `item1` wider, spanning from col line 1 to col line 3 (i.e. two regular item slots)

### Grid container

- `grid-template-columns` defines number of cols in the grid layout, and can also define the width of each col
    - takes in a space-separated list, each value defining the length of the respective col
- `grid-template-rows`
- `justify-content` horizontally aligns the whole grid inside the container
- `align-content` vertically aligns the whole grid inside the container

### Grid items

- `grid-column` property defines the starting and ending column lines
    ```
    .item1 { grid-column: 1 / 5; }
    .item2 { grid-column: 2 / span 3 }
    ```
    - item1 starts on col-line 1 and end on col-line 5
    - item2 starts on col-line 2 and **spans** 3 columns
- `grid-row` is for rows; `grid-area` is shorthand
- ```
  grid-area: 1 / 2 / 5 / 6
  ```
    - Format is `row-line-start / col-line / row-line-end / col-line-end`
    - Can also be used along with `grid-template-areas` to name areas

## Variables

- `var()` function used to insert the value of a custom property
- Define **variables** within a CSS selector to define its scope

    ```
    :root { --main-bg-color: blue; }
    #div1 { background-color: var(--main-bg-color); }
    ```




