# CSS Theory Assignment — Week 2
## MERN Stack + AI Engineering Bootcamp 



## Q1. What is CSS and how do you add it to an HTML page?


### What is CSS?

CSS stands for **Cascading Style Sheets**. It is a stylesheet language used to control the **visual presentation** of HTML elements on a webpage — things like colors, fonts, layout, spacing, and responsiveness.

**The problem CSS solves:** Without CSS, every webpage would look like a plain text document. HTML defines the *structure* (what is on the page), while CSS defines the *style* (how it looks). Separating structure from style makes code cleaner, reusable, and easier to maintain.



### Three Ways to Add CSS to an HTML Document

| Method | How It Works | When to Use |
|--------|-------------|-------------|
| **External CSS** | A separate `.css` file linked via `<link>` tag | ✅ Recommended for real projects |
| **Internal CSS** | CSS written inside `<style>` tag in `<head>` | Small single-page projects or testing |
| **Inline CSS** | CSS written directly on an element via `style=""` | Quick fixes or dynamic JS styling only |

---

### Method 1: External CSS (Recommended ✅)

**index.html**
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>My Page</title>
    <link rel="stylesheet" href="styles.css">
  </head>
  <body>
    <h1>Hello World</h1>
  </body>
</html>
```

**styles.css**
```css
h1 {
  color: navy;
  font-size: 2rem;
}
```

**Why it's preferred:** One CSS file can style hundreds of HTML pages. Changing one file updates the entire website. The browser also caches external files for faster load times.

---

### Method 2: Internal CSS

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <style>
      h1 {
        color: navy;
        font-size: 2rem;
      }
    </style>
  </head>
  <body>
    <h1>Hello World</h1>
  </body>
</html>
```

---

### Method 3: Inline CSS

```html
<h1 style="color: navy; font-size: 2rem;">Hello World</h1>
```

**Why inline CSS is avoided:** It mixes structure with style, is hard to maintain, cannot be reused, and overrides external/internal styles making debugging difficult.

---

## Q2. Explain CSS Selectors with examples.


CSS selectors are patterns used to **target HTML elements** and apply styles to them.

### All Seven Selector Types

| Selector | Syntax | Targets | Specificity |
|----------|--------|---------|-------------|
| **Element** | `p` | All `<p>` tags | Low |
| **Class** | `.box` | Elements with `class="box"` | Medium |
| **ID** | `#header` | Element with `id="header"` | High |
| **Group** | `h1, h2, p` | Multiple selectors at once | Varies |
| **Descendant** | `div p` | Any `<p>` inside a `<div>` | Medium |
| **Child** | `div > p` | Direct child `<p>` of `<div>` only | Medium |
| **Universal** | `*` | Every element on the page | None (0) |

---

### Code Task: CSS rules using all seven selector types

```css
/* 1. Element Selector — targets all <h2> tags */
h2 {
  font-family: Georgia, serif;
  color: #333;
}

/* 2. Class Selector — targets elements with class="card" */
.card {
  background-color: #f9f9f9;
  padding: 20px;
  border-radius: 8px;
}

/* 3. ID Selector — targets <div id="main-header"> */
#main-header {
  background-color: #1a1a2e;
  color: white;
  padding: 40px;
}

/* 4. Group Selector — applies same style to h1, h2, and h3 */
h1, h2, h3 {
  font-weight: bold;
  margin-bottom: 10px;
}

/* 5. Descendant Selector — targets any <p> anywhere inside .container */
.container p {
  line-height: 1.8;
  color: #555;
}

/* 6. Child Selector — targets only DIRECT <li> children of <ul> */
ul > li {
  list-style: square;
  padding: 5px 0;
}

/* 7. Universal Selector — targets every element */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
```

---

### Class vs ID — Key Differences

| | Class (`.`) | ID (`#`) |
|--|-------------|----------|
| Reusability | ✅ Can be used on many elements | ❌ Must be unique per page |
| Specificity | Lower | Higher |
| Use case | Reusable styles (cards, buttons) | Unique sections (header, footer) |

**Rule:** Use a **class** when you'll apply the same style to multiple elements. Use an **ID** only once per page — primarily for JavaScript targeting or page anchors.

**Descendant vs Child:** `div p` selects ALL `<p>` elements inside a div (even deeply nested), while `div > p` only selects `<p>` elements that are **direct children** — one level deep.

---

## Q3. What is the CSS Box Model? Explain each layer.


Every HTML element is treated as a **rectangular box** made up of four layers, from innermost to outermost:

```
+------------------------------------------+
|               MARGIN (outside)           |
|  +------------------------------------+  |
|  |          BORDER                    |  |
|  |  +------------------------------+  |  |
|  |  |        PADDING               |  |  |
|  |  |  +------------------------+  |  |  |
|  |  |  |       CONTENT          |  |  |  |
|  |  |  |   (text, images)       |  |  |  |
|  |  |  +------------------------+  |  |  |
|  |  +------------------------------+  |  |
|  +------------------------------------+  |
+------------------------------------------+
```

### The Four Layers

| Layer | Description | Controlled By |
|-------|-------------|---------------|
| **Content** | The actual text or image (innermost) | `width`, `height` |
| **Padding** | Space *inside* the border, between content and border | `padding` |
| **Border** | The visible line around the padding | `border` |
| **Margin** | Space *outside* the border, between elements | `margin` |

- **Padding is inside the border** — it takes the element's background color.
- **Margin is outside the border** — it is always transparent.
- **Which layer is innermost?** Content.

---

### box-sizing: content-box vs border-box

| | `content-box` (default) | `border-box` (recommended ✅) |
|--|------------------------|-------------------------------|
| `width` applies to | Content only | Content + padding + border |
| Actual rendered width | width + padding + border | Exactly `width` as set |
| Predictability | Confusing | Easy to reason about |

**Example:** If you set `width: 300px; padding: 20px; border: 2px solid`:
- `content-box` → actual width = 300 + 40 + 4 = **344px**
- `border-box` → actual width = **300px** (padding and border fit inside)

**Professional projects always use `border-box`** because it makes layouts predictable.

---

### Code Task

```css
.box {
  width: 300px;
  padding: 20px;
  border: 2px solid black;
  margin: 16px;
  box-sizing: border-box;
  /* Total rendered width = exactly 300px */
  /* Total space taken (with margin) = 300 + 16 + 16 = 332px */
}
```

---

## Q4. Explain CSS Colors. What are the different ways to define a color?


CSS supports **five color formats**. Every format can express any color, but they differ in features and use cases.

### All Five Color Formats Compared

| Format | Syntax | Supports Transparency | Best For |
|--------|--------|-----------------------|----------|
| **Named** | `color: red` | ❌ | Quick prototyping |
| **HEX** | `color: #F97316` | ✅ (with 8-digit HEX) | Design systems, most common |
| **RGB** | `color: rgb(249, 115, 22)` | ❌ | When you know RGB values |
| **RGBA** | `color: rgba(249, 115, 22, 0.5)` | ✅ | Transparent overlays |
| **HSL** | `color: hsl(25, 95%, 53%)` | ✅ (with HSLA) | Theming, easy to adjust |

**Most commonly used by developers:** HEX — it's short, precise, and used in virtually every design tool (Figma, Photoshop, etc.).

**What does the 'A' in RGBA stand for?** Alpha — which controls transparency. `0` = fully transparent, `1` = fully opaque.

---

### Code Task: Orange color `#F97316` in all five formats

```css
/* 1. Named Color (approximate — no exact named match for this orange) */
.named   { color: orange; }

/* 2. HEX */
.hex     { color: #F97316; }

/* 3. RGB */
.rgb     { color: rgb(249, 115, 22); }

/* 4. RGBA (50% transparent) */
.rgba    { color: rgba(249, 115, 22, 1); }

/* 5. HSL — Hue 25°, Saturation 95%, Lightness 53% */
.hsl     { color: hsl(25, 95%, 53%); }
```

---

### opacity: 0.5 vs rgba(0, 0, 0, 0.5)

| | `opacity: 0.5` | `rgba(0,0,0,0.5)` |
|--|----------------|-------------------|
| What becomes transparent | **Entire element** including all child elements | **Only that specific color property** |
| Affects children? | ✅ Yes — children inherit opacity | ❌ No — children are unaffected |
| Use case | Fading an entire card/image | Transparent background or text only |

**Does opacity affect child elements?** Yes. Setting `opacity: 0.5` on a parent makes all its children 50% transparent too — you cannot override this with CSS.

**Does rgba affect child elements?** No. `background: rgba(0,0,0,0.5)` only makes the background transparent; child elements remain fully visible.

---

## Q5. What are CSS Units? Explain px, %, rem, em, vh, and vw.


### All Six Units Explained

| Unit | Relative To | Practical Use Case | Example |
|------|-------------|-------------------|---------|
| **px** | Fixed — screen pixels | Borders, shadows, exact sizes | `border: 2px solid` |
| **%** | Parent element's size | Fluid widths, responsive containers | `width: 50%` |
| **rem** | Root element (`<html>`) font-size (default 16px) | Font sizes, spacing | `font-size: 1.5rem` = 24px |
| **em** | Current element's font-size | Padding/margin relative to text | `padding: 1em` |
| **vh** | 1% of viewport height | Full-screen sections | `height: 100vh` |
| **vw** | 1% of viewport width | Full-width banners | `width: 100vw` |

---

### Key Concepts

- **What is 1rem equal to by default?** 16px (the browser default for `<html>` font-size). So `2rem = 32px`, `0.5rem = 8px`.
- **% is relative to** the **parent element**, not the root (unlike rem).
- **vh stands for** Viewport Height — 100vh = 100% of the visible browser window height.
- **Why is rem better than px for font-size accessibility?** Users can change their browser's default font size. If you use `rem`, your text scales with it. If you use `px`, it stays fixed and ignores the user's accessibility preferences.

---

### The Golden Rule

| Property | Preferred Unit | Reason |
|----------|---------------|--------|
| **Font sizes** | `rem` | Respects user accessibility settings |
| **Widths** | `%` or `rem` | Fluid and responsive |
| **Full-screen sections** | `vh` / `vw` | Fills exactly the viewport |
| **Borders, shadows** | `px` | Precise, should not scale |

---

### Code Task: Hero section — full viewport height, font-size scales with viewport, max-width uses rem

```css
.hero {
  /* Full viewport height */
  height: 100vh;

  /* Font size scales with viewport width */
  font-size: clamp(1rem, 2.5vw, 2rem);

  /* Max width uses rem for accessibility */
  max-width: 75rem; /* = 1200px at default font size */
  margin: 0 auto;

  /* Layout */
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  background-color: #1a1a2e;
  color: white;
}

.hero h1 {
  font-size: clamp(2rem, 5vw, 4rem);
  margin-bottom: 1rem;
}

.hero p {
  font-size: 1.25rem; /* rem — accessible */
}
```

---

## Q6. What is CSS Specificity and how does the Cascade work?


When multiple CSS rules target the same element, the browser must decide which rule wins. This is determined by **specificity** and the **cascade**.

### Specificity — How It's Calculated

Specificity is calculated as a **score with four columns: (inline, ID, class/pseudo-class/attr, element)**

| Selector Type | Score | Example |
|--------------|-------|---------|
| Inline style | **1,0,0,0** | `style="color: red"` |
| ID | **0,1,0,0** | `#header` |
| Class / Pseudo-class / Attribute | **0,0,1,0** | `.card` / `:hover` / `[type]` |
| Element / Pseudo-element | **0,0,0,1** | `p` / `::before` |
| Universal | **0,0,0,0** | `*` |

**Which has higher specificity — class or element?** Class (`0,0,1,0`) beats element (`0,0,0,1`).

**What specificity score does an inline style have?** `1,0,0,0` — the highest (without `!important`).

---

### How the Cascade Works

The cascade is the algorithm browsers use to resolve style conflicts. It follows this priority order:

1. **Origin** — Browser default < Author CSS < Inline styles
2. **Specificity** — Higher score wins
3. **Source Order** — If specificity is equal, the rule that appears **later** in the CSS file wins

**If two rules have equal specificity, which one wins?** The one that appears later (lower) in the CSS file.

---

### What does `!important` do?

`!important` overrides the normal cascade and forces a rule to win regardless of specificity.

```css
p { color: blue !important; } /* wins even against inline styles */
```

**Why it should be avoided:**
- It breaks the natural cascade, making CSS harder to debug
- It can only be overridden by another `!important` with higher specificity — creating a war
- It makes styles unpredictable and unmaintainable

Use it only as a last resort (e.g., overriding third-party library styles).

---

### Code Task: `<p id="intro" class="text">Hello</p>` — three rules targeting it differently


/* Rule 1: Element selector — specificity 0,0,0,1 */
p {
  color: green;
}

/* Rule 2: Class selector — specificity 0,0,1,0 — WINS over Rule 1 */
.text {
  color: blue;
}

/* Rule 3: ID selector — specificity 0,1,0,0 — WINS over Rules 1 and 2 */
#intro {
  color: red; /* This color wins */
}


**Which colour wins?** `red` — because `#intro` has the highest specificity score (`0,1,0,0`).

**Specificity comparison:** `#intro` (0,1,0,0) > `.text` (0,0,1,0) > `p` (0,0,0,1)


## Q7. Explain CSS Flexbox. How does it differ from block layout?


# What is Flexbox?

Flexbox (**Flexible Box Layout**) is a **1-dimensional layout system** — it lays elements out in either a **row** or a **column**. When you set `display: flex` on a container, all its direct children automatically become **flex items** that can grow, shrink, and align intelligently.



### Flexbox vs Block Layout

| Feature | Block Layout | Flexbox |
|---------|-------------|---------|
| Direction | Vertical only (top to bottom) | Row OR column |
| Horizontal centering | Requires `margin: 0 auto` | `justify-content: center` |
| Vertical centering | Very difficult | `align-items: center` |
| Equal-height columns | Nearly impossible | Default behavior |
| Reordering elements | Not possible in CSS | `order` property |


### Key Flexbox Properties

```css
.container {
  display: flex;

  /* Direction of the main axis */
  flex-direction: row;          /* row | row-reverse | column | column-reverse */

  /* Alignment along MAIN axis (horizontal if row) */
  justify-content: space-between; /* flex-start | center | space-between | space-around | space-evenly */

  /* Alignment along CROSS axis (vertical if row) */
  align-items: center;          /* flex-start | flex-end | center | stretch | baseline */

  /* Wrapping */
  flex-wrap: wrap;              /* wrap items to next line if they don't fit */

  /* Gap between items */
  gap: 16px;
}

.item {
  /* flex: 1 means this item grows to fill available space equally */
  flex: 1;
  /* flex is shorthand for: flex-grow flex-shrink flex-basis */
  /* flex: 1 = flex: 1 1 0% */
}
```

---

justify-content vs align-items

| Property | Controls | Axis |
|----------|----------|------|
| `justify-content` | Spacing and alignment of items along **main axis** (default: horizontal) | Main axis |
| `align-items` | Alignment of items along **cross axis** (default: vertical) | Cross axis |

**How to center an element both horizontally and vertically:**
```css
.container {
  display: flex;
  justify-content: center; /* horizontal center */
  align-items: center;     /* vertical center */
  height: 100vh;
}
```

**What does `flex-wrap: wrap` do?** By default, flex items all try to fit on one line. `flex-wrap: wrap` allows them to wrap onto multiple lines when they don't fit, maintaining their minimum widths.

**What does `flex: 1` do?** It makes an item grow to fill all available space. If multiple items have `flex: 1`, they share the space equally.

---

### Real-World Use Cases

1. **Navigation bar** — logo on the left, links on the right
2. **Card grid** — equal-height cards in a row that wrap on small screens

---

### Code Task: CSS Navbar — logo left, links right, vertically centred, gap between links

```css
/* HTML Structure:
<nav class="navbar">
  <div class="logo">MyBrand</div>
  <ul class="nav-links">
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
*/

.navbar {
  display: flex;
  justify-content: space-between; /* logo left, links right */
  align-items: center;            /* vertically centred */
  padding: 0 2rem;
  height: 64px;
  background-color: #1a1a2e;
}

.logo {
  color: #F97316;
  font-size: 1.5rem;
  font-weight: bold;
}

.nav-links {
  display: flex;
  gap: 24px; /* gap between links */
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav-links a {
  color: white;
  text-decoration: none;
  font-size: 1rem;
  transition: color 0.2s ease;
}

.nav-links a:hover {
  color: #F97316;
}
```

---

## Q8. What are CSS Pseudo-classes and Pseudo-elements?


### Key Difference: `:` vs `::`

| | Pseudo-class (`:`) | Pseudo-element (`::`) |
|--|-------------------|----------------------|
| Syntax | Single colon `:` | Double colon `::` |
| Targets | **State** of an element | **Virtual part** of an element |
| Examples | `:hover`, `:focus`, `:nth-child()` | `::before`, `::after`, `::placeholder` |
| Adds real HTML? | No | No — only visual content |

---

### Pseudo-classes — Styling by State

```css
/* :hover — when mouse is over the element */
button:hover {
  background-color: orange;
  cursor: pointer;
}

/* :focus — when element is focused (tabbed to or clicked) */
input:focus {
  outline: 2px solid #F97316;
  border-color: #F97316;
}

/* :nth-child() — select elements by position */
li:nth-child(2n)  { background: #f0f0f0; } /* every even item */
li:nth-child(3n)  { background: #e0e0e0; } /* every 3rd item */

/* :not() — select elements that do NOT match */
p:not(.special) {
  color: gray;
}
```

**What does `:nth-child(2n)` select?** Every even-numbered child (2nd, 4th, 6th...). `2n` means "multiples of 2."

**How to style every 3rd list item?** `:nth-child(3n)` — matches 3rd, 6th, 9th, etc.

---

### Pseudo-elements — Styling Virtual Parts

```css
/* ::before — inserts virtual content BEFORE the element's content */
.featured::before {
  content: "★ "; /* content property is REQUIRED for ::before/::after to appear */
  color: #F97316;
}

/* ::after — inserts virtual content AFTER the element's content */
.badge::after {
  content: " NEW";
  font-size: 0.75rem;
  background: green;
  color: white;
  padding: 2px 6px;
  border-radius: 4px;
}

/* ::placeholder — styles the placeholder text in input fields */
input::placeholder {
  color: #999;
  font-style: italic;
}
```

**Does `::before` add a real HTML element?** No — it creates a **virtual element** that exists only visually. It cannot be selected in the DOM by JavaScript.

**What CSS property is required for `::before`/`::after` to appear?** The `content` property — even if it's empty (`content: ""`). Without it, the pseudo-element is not rendered at all.

---

### Code Task: Button turns orange on hover + ★ before .featured items + grey placeholder

```css
/* Button turns orange on hover */
button:hover {
  background-color: orange;
  color: white;
  transition: background-color 0.3s ease;
}

/* ★ before every .featured list item */
li.featured::before {
  content: "★ ";
  color: gold;
}

/* Style placeholder text grey in inputs */
input::placeholder {
  color: #999;
  font-style: italic;
}
```

---

## Q9. Explain CSS Transitions and Animations.


### Transitions vs Animations

| Feature | Transitions | Animations (`@keyframes`) |
|---------|-------------|--------------------------|
| Trigger needed | ✅ Yes (hover, focus, JS class) | ❌ No — can run automatically |
| Control | Start/end state only | Full control over every step |
| Direction | A → B | Any sequence: A → B → C → A |
| Looping | ❌ Not easily | ✅ `animation-iteration-count: infinite` |
| Use case | Hover effects, state changes | Loading spinners, page-load reveals |

---

### Transitions

**Transition shorthand:** `transition: property duration timing-function delay`

```css
.button {
  background-color: #1a1a2e;
  transform: translateY(0);
  transition: background-color 0.3s ease, transform 0.3s ease-out;
  /* Yes — you can have multiple transitions on one element using commas */
}

.button:hover {
  background-color: #F97316;
  transform: translateY(-4px);
}
```

### Timing Functions

| Function | Behaviour |
|----------|-----------|
| `ease` | Starts slow, speeds up, ends slow (default) |
| `ease-in` | Starts slow, ends fast |
| `ease-out` | Starts fast, ends slow (most natural-looking) |
| `linear` | Constant speed throughout |

**Common triggers for transitions:** `:hover`, `:focus`, `:active`, JavaScript adding/removing a class.

---

### Animations with `@keyframes`

```css
/* Define the keyframes */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Animation shorthand: name duration timing delay iteration direction fill-mode */
.card {
  animation: fadeInUp 0.6s ease-out 0s 1 normal forwards;
}
```

**What does `animation-iteration-count: infinite` do?** Makes the animation repeat forever without stopping. Used for loaders, pulsing effects.

**What does `animation-fill-mode: forwards` do?** Keeps the element in the state of the **last keyframe** after the animation ends. Without it, the element snaps back to its original styles.

---

### Why prefer transform and opacity for animations?

`transform` (translateY, scale, rotate) and `opacity` are **GPU-accelerated** — the browser handles them without recalculating the layout. Animating `width`, `margin`, or `height` triggers **layout recalculation (reflow)**, which is slow and causes jank/flickering.

---

### Code Task: Card that lifts on hover + CSS fade-in animation on page load

```css
/* HTML: <div class="card">Content</div> */

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.card {
  background: white;
  padding: 24px;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);

  /* Page-load fade-in animation */
  animation: fadeInUp 0.6s ease-out forwards;

  /* Smooth hover transition */
  transition: transform 0.3s ease-out, box-shadow 0.3s ease-out;
}

.card:hover {
  /* Lifts up */
  transform: translateY(-8px);
  /* Shadow deepens to reinforce the lifted feel */
  box-shadow: 0 12px 32px rgba(0, 0, 0, 0.15);
}
```

---

## Q10. What is Responsive Web Design? Explain Media Queries, CSS Variables, and Mobile-First approach.


### Part A — Media Queries

A **media query** allows you to apply CSS rules only when certain conditions about the device or viewport are met.

**Syntax:**
```css
@media (condition) {
  /* CSS rules applied only when condition is true */
}
```

**Standard industry breakpoints:**

| Breakpoint | Min-width | Target |
|-----------|-----------|--------|
| Mobile | default (no query) | 0px–767px |
| Tablet | `768px` | 768px–1023px |
| Laptop | `1024px` | 1024px–1279px |
| Desktop | `1280px` | 1280px+ |

---

### Part B — Mobile-First Approach

**Mobile-first** means you write your **base CSS for small screens first**, then use `min-width` media queries to add styles as screen size increases.

**Mobile-first uses `min-width`** — you start small and scale UP.

| | Mobile-First (`min-width`) | Desktop-First (`max-width`) |
|--|---------------------------|----------------------------|
| Default styles target | Small screens | Large screens |
| Media queries used | `min-width` | `max-width` |
| Performance | ✅ Better — mobile loads less CSS | ❌ Worse — mobile downloads all CSS |
| Industry standard | ✅ Yes | ❌ Old approach |

**Why mobile-first is the industry standard:** More than 60% of web traffic is mobile. Starting with mobile forces you to prioritize content and performance from the start.

---

### Part C — CSS Variables (Custom Properties)

CSS variables are **reusable values** defined with `--` and used with `var()`.

```css
/* Define in :root so they're globally available */
:root {
  --color-primary: #F97316;
  --color-bg: #ffffff;
  --color-text: #1a1a2e;
  --font-size-base: 1rem;
  --spacing-md: 1.5rem;
}

/* Use with var() */
.button {
  background-color: var(--color-primary);
  padding: var(--spacing-md);
  font-size: var(--font-size-base);
}

/* var(--color, fallback) — fallback if variable not defined */
.card {
  color: var(--color-text, black); /* uses black if --color-text is missing */
}
```

**Difference between `var(--color)` and `var(--color, fallback)`:** The second argument is a fallback value used if the variable is undefined or invalid.

**Can JavaScript read and change CSS variables?** Yes.
```javascript
// Read
getComputedStyle(document.documentElement).getPropertyValue('--color-primary');

// Write
document.documentElement.style.setProperty('--color-primary', '#3b82f6');
```

---

### Code Task: Design system in :root + dark mode + mobile-first media queries

```css
/* ===== DESIGN SYSTEM IN :ROOT ===== */
:root {
  /* Colors */
  --color-bg: #ffffff;
  --color-text: #1a1a2e;
  --color-primary: #F97316;
  --color-card-bg: #f9f9f9;
  --color-border: #e2e8f0;

  /* Font sizes */
  --font-size-sm: 0.875rem;
  --font-size-base: 1rem;
  --font-size-lg: 1.25rem;
  --font-size-xl: 2rem;

  /* Spacing */
  --spacing-sm: 0.5rem;
  --spacing-md: 1rem;
  --spacing-lg: 2rem;
  --spacing-xl: 4rem;
}

/* ===== DARK MODE via data-theme attribute ===== */
[data-theme='dark'] {
  --color-bg: #0f0f1a;
  --color-text: #e2e8f0;
  --color-card-bg: #1a1a2e;
  --color-border: #2d3748;
}

/* Also respect OS-level dark mode preference */
@media (prefers-color-scheme: dark) {
  :root {
    --color-bg: #0f0f1a;
    --color-text: #e2e8f0;
    --color-card-bg: #1a1a2e;
    --color-border: #2d3748;
  }
}

/* What does @media (prefers-color-scheme: dark) do?
   It detects if the user has set their OS to dark mode
   and applies dark styles automatically */

/* ===== BASE STYLES (Mobile-First — default is mobile) ===== */
body {
  background-color: var(--color-bg);
  color: var(--color-text);
  font-size: var(--font-size-base);
  margin: 0;
  padding: var(--spacing-md);
  font-family: system-ui, sans-serif;
}

.container {
  width: 100%;
  padding: 0 var(--spacing-md);
}

.grid {
  display: grid;
  grid-template-columns: 1fr; /* 1 column on mobile */
  gap: var(--spacing-md);
}

.hero-title {
  font-size: var(--font-size-xl);
}

/* ===== TABLET — 768px and above ===== */
@media (min-width: 768px) {
  .container {
    max-width: 768px;
    margin: 0 auto;
  }

  .grid {
    grid-template-columns: repeat(2, 1fr); /* 2 columns on tablet */
  }

  .hero-title {
    font-size: 2.5rem;
  }
}

/* ===== DESKTOP — 1024px and above ===== */
@media (min-width: 1024px) {
  .container {
    max-width: 75rem; /* 1200px */
  }

  .grid {
    grid-template-columns: repeat(3, 1fr); /* 3 columns on desktop */
  }

  .hero-title {
    font-size: 3.5rem;
  }
}
```

---

