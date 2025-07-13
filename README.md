# Project HTML CSS - Form

## Lab Description

In this lab exercise we will create a sign-up form using HTML and CSS.  

![Form Mockup](img/form-mockup.png)

The form is not connected to a backend to processes sign-ups.

## Demo

The demo website is live here

https://ebouchut-laplateforme.github.io/project-html-css-form/

It is published automatically each time we push to the `main` branch.

## Layout

I use a mix of CSS Flexbox and grid layout:
- Flexbox to lay out:
    -  The topmost items from right to left (heading 1, and form)
    -  The first name and last name fields in the form from left to right
- Grid layout for the the form

### 2-Column Layout using Flexbox

The `<body>` tag is a flex container (`display: flex;`) that lays its flex items (direct children) horizontally from right to left (`flex-direction: row-reverse;`).

- First, the `<header>` with a `<h1>` is displayed on the right
- Then, `<main>` that contains the `<form>` is displayed on the left

```mermaid
flowchart TB
    subgraph body
        direction RL

        header["&lt;header&gt;&lt;h1&gt;..."]
        main["&lt;main&gt;&lt;section&gt;&lt;form&gt;..."]

         header --> main
    end
```

- [HTML](https://github.com/ebouchut-laplateforme/project-html-css-form/blob/de9aa0f95999fc959570fe675cc84a0cfab4aefc/index.html#L12-L21)
  ```html
  <body class="flex-container-body center">
  
      <header class="flex-item-body">
          <h1> <!-- ... --> </h1>
      </header>

    <main class="flex-item-body">
        <section>
            <form action="#" method="post" autocomplete="off" id="grid-container-form">
                <!-- ... -->
            </form>
          </section>
      </main>
  </body>
  ```
- [CSS](https://github.com/ebouchut-laplateforme/project-html-css-form/blob/de9aa0f95999fc959570fe675cc84a0cfab4aefc/css/styles.css#L76-L78)
  ```css
  .flex-container-body { /* body */*
      display:        flex;
      flex-direction: row-reverse;
  }
  ```

The 2 flex item (`<header>`, `<main>`) take [a share of the available width](https://github.com/ebouchut-laplateforme/project-html-css-form/blob/de9aa0f95999fc959570fe675cc84a0cfab4aefc/css/styles.css#L84C4-L96):
- 30%: `<header>` (contains `<h1>`)  
  ```css
    .flex-item-body:first-child {
    /* header(h1) takes 30% of its container width (body),
     * minus half the width of the gutter around it
     */
    flex:            calc(30% - (var(--ex-container-items-gap) / 2));
  }
  ```
- 70%: `<main>`   (contains  `<form>`)
  ```css
  .flex-item-body:nth-child(2) {
    /* main(section > form) takes 70% of its container width (body),
     * minus half the width of the gutter around it
     */
    flex:            calc(70% - (var(--ex-container-items-gap) / 2));
  }
  ```

I use [nested CSS rules](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_nesting/Using_CSS_nesting) to target flex items within their container, improving readability by keeping related rules close together and in context.

```css
.flex-container-body {
  display:         flex;
  /* The flex items are laid out from right to left (main(section > form) ← header(h1)  */
  flex-direction:  row-reverse;
  flex-wrap:       wrap;
  justify-items:   center; /* Center each flex item horizontally */
  align-items:     center; /* Center each flex item vertically */
  gap:             var(--ex-container-items-gap); /* Add a gutter between the flex items */

  .flex-item-body:first-child {
    /* header(h1) takes 30% of its container width (body),
     * minus half the width of the gutter around it
     */
    flex:            calc(30% - (var(--ex-container-items-gap) / 2));
  }

  .flex-item-body:nth-child(2) {
    /* main(section > form) takes 70% of its container width (body),
     * minus half the width of the gutter around it
     */
    flex:            calc(70% - (var(--ex-container-items-gap) / 2));
  }
}
```

### Grid Layout for the Form

TODO:

### Flexbox Layout for the Full Name

The **first name** and **last name** form fields (that I refer to as he full name) should be displayed next to each other from left to right.

![Full Name](./img/full-name-flexbox.png)

[CSS](https://github.com/ebouchut-laplateforme/project-html-css-form/blob/de9aa0f95999fc959570fe675cc84a0cfab4aefc/css/styles.css#L116-L118)
  ```css
  #grid-container-form {
    display:               grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows:    auto;
    justify-items:         start; /* By default grid items are left aligned */
  
    padding: 1em;
  
    /* ... */
  
    & > .full-name {       /* fieldset with first-name and last-name fields */
      display:             flex;
      flex-direction:      flex-start;
      /* ... */
    }
  ```
- [HTML](https://github.com/ebouchut-laplateforme/project-html-css-form/blob/de9aa0f95999fc959570fe675cc84a0cfab4aefc/index.html#L24-L33)
  I used the dreaded `<div>`s here to act as layout containers. First they have no semantic meaning and I have used before all the semantic tags available to me ;-)!
  ```html
  <main class="flex-item-body">
    <section>
      <form action="#" method="post" autocomplete="off" id="grid-container-form">
        <legend>Sign Up</legend>

        <fieldset class="full-name">
          <div>
            <label for="first-name" class=""first-name">First Name</label>
            <input type="text" id="first-name" name="first-name">
          </div>
          <div>
            <label for="last-name" class="last-name">Last Name</label>
            <input type="text" id="last-name" name="last-name">
          </div>
        </fieldset>
  ```
