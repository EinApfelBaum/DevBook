---
created: 29.07.2021
tags: typescript react html
---

# Dropdown in react/typescript with html

```typescript
const style: CSSProperties = {
    width: 80,
    marginLeft: 10,
    marginRight: 20,
    height: 40
  };

interface DropdownOption  {
    key:string,
    text:string,
    value: string
}

const options: DropdownOption[] = [
    {
      key: '10',
      text: '10',
      value: '10'
    },
    {
      key: '25',
      text: '25',
      value: '25'
    }
  ]

const handleOnChange= (event: ChangeEvent<HTMLSelectElement>) => {
  console.log(event.target.value)
}
```

```html
<select id='dropdown' onChange={handleOnChange} style={style}>
    {
    options.map(item => {
    return <option value={item.value} key={item.key}> {item.text}</option>
    })
}
</select>
```
