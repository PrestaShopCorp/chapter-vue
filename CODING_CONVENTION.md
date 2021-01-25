# Coding Convention !

**At prestashop we use TypeScript in FRONT**

## Component option order

1.  **The first/mandatory one**
    - `name`
2.  **Template Dependencies**

    - `components`
    - `directives`

3.  **Composition**

    - `extends`
    - `mixins`
    - `provide`/`inject`

4.  **Interface**

    - `inheritAttrs`
    - `props`
    - `emits`

5.  **Composition API**

    - `setup`

6.  **Local State**

    - `data`
    - `computed`

7.  **Events**

    - `watch`
    - Lifecycle Events (in the order they are called)
      - `beforeCreate`
      - `created`
      - `beforeMount`
      - `mounted`
      - `beforeUpdate`
      - `updated`
      - `activated`
      - `deactivated`
      - `beforeUnmount`
      - `unmounted`
      - `errorCaptured`
      - `renderTracked`
      - `renderTriggered`

8.  **Non-Reactive Properties**

    - `methods`

## Props naming

camelCase in javascript

```javascript
props: {
  messageIntro: String;
}
```

kebab-case in html template

```html
<welcome-message message-intro="hi"></welcome-message>
```

camelCase in JSX

```javascript
<WelcomeMessage messageIntro="hi" />
```

## Multiple attribute

in html template

```html
<img src="logo.png" alt="logo" />
```

````html
<my-component jane="a" doe="b"></my-component>
```javasript in JSX
<img src="logo.png" alt="logo" />
````

```html
<MyComponent foo="a" bar="b" baz="c" />
```

## Expressions in templates

Never make a transformation directly in the template or in the JSX. **Prefer the use of computed**.

### Bad

```javascript
{
  {
    fullName
      .split(" ")
      .map((word) => {
        return word[0].toUpperCase() + word.slice(1);
      })
      .join(" ");
  }
}
```

### Good

```html
<!-- In a template -->
{{ normalizedFullName }}
```

```javascript
// in JSX
{
  normalizedFullName;
}
```

```javascript
computed: {
  normalizedFullName() {
    return this.fullName.split(' ')
      .map(word => word[0].toUpperCase() + word.slice(1))
      .join(' ')
  }
}
```

## Complexe computed

You should always (if possible) split a computed into several parts. **A computed should be a simple treatment.**
example :

```javascript
computed: {
  price() {
    const basePrice = this.manufactureCost / (1 - this.profitMargin)
    return (
      basePrice -
      basePrice * (this.discountPercent || 0)
    )
  }
}
```

to

```javascript
computed: {
  basePrice() {
    return this.manufactureCost / (1 - this.profitMargin)
  },

  discount() {
    return this.basePrice * (this.discountPercent || 0)
  },

  finalPrice() {
    return this.basePrice - this.discount
  }
}
```

## Props definition

**You must type your props and if possible have validators on them. **

```javascript
props: {
  status: {
    type: String,
    required: true,

    validator: value => {
      return [
        'syncing',
        'synced',
        'version-conflict',
        'error'
      ].includes(value)
    }
  }
}
```

### Never use

```javascript
props: ["status"];
```
