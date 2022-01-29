---
created: 29.07.2021
tags: typescript CSS react
---

# Define a style in a component

```typescript
const dropdownStyle: CSSProperties = {
    width: 80,
    marginLeft: 10,
    marginRight: 20,
    height: 40
  };

// store multiple css styles 
export interface StylesDictionary{
    [Key: string]: CSSProperties;
}
```

```html
<select id='dropdown' style={dropdownStyle}>
```
