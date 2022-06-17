
### Contents

- [Convert a NodeList to an Array](#convert-a-nodelist-to-an-array)
- [Use setTimeout on Promise chain](#use-settimeout-on-promise-chain)
- [Rename Key From Object (Function)](#rename-key-from-object-function)

---

### Convert a NodeList to an Array

```html
<div class="element"></div>
<div class="element"></div>
```

```javascript
let elements = [...document.querySelectorAll('.element')]
```

Output

```
Array(2) [div.element, div.element]
```

---

### Use setTimeout on Promise chain

```javascript
const delay = (milliseconds) => {
    return new Promise((resolve) => window.setTimeout(resolve, milliseconds))
}
```

---

### Rename Key From Object (Function)

```javascript
Object.defineProperty(Object.prototype, 'rename', {
    configurable: false,
    enumerable:   false,
    writable:     false,
    value: (oldKey, newKey) => {
        if (this[newKey] !== undefined) {
            throw `Cannot rename to '${newKey}' key as this key already exists.`;
        }

        if (this[oldKey] !== undefined) {
            this[newKey] = this[oldKey];
            delete this[oldKey];
        }

        return this;
    }
});
```
