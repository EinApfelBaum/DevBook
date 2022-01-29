---
created: 06.08.2021
tags: html CSS
---

# HTML nested list

![nested list](/assets/images/2021-08-06-11-56-28.png)

```css
ol {
  counter-reset: item;
}
ol li {
  display: block;
}
ol li:before {
  content: counters(item, ". ") ". ";
  counter-increment: item;
}
```

```html
<ol>

    <li>Parent 1 <!-- Parent open li tag -->
        <ol> 
            <li>Child</li>
        </ol>
    </li> <!-- Parent close li tag -->

    <li>Parent 2</li>
</ol>
```

> ⚠️
> The nested list must included into the parent `<li>` element!

## ❌ This will not work

```html
<ol>
    <li>Parent 1</li>
    <ol> 
        <li>Child</li>
    </ol>
    <li>Parent 2</li>
</ol>
```
