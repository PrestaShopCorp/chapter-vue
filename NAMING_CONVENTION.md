# Naming Convention !

Improving the readability of your project !

## Component Files

Correct component naming allows you to find a component faster when you need to modify it or review its usage mode.

### Random Component

#### Bad

```javascript
Vue.component('TodoList', { // ... })
Vue.component('TodoItem', { // ... })
```

#### Good

```javascript
components/
|- TodoList.js
|- TodoItem.js
```

Never write the name of a component in lower case or camelcase.

#### Bad

```javascript
components/
|- mycomponent.vue
```

#### or

```
components/
|- myComponent.vue
```

#### Good

```
components/
|- MyComponent.vue
```

#### or

```
components/
|- my-component.vue
```

### Base Component

Base components that apply app-specific styling and conventions should all begin with a specific prefix, such as `Base`, `App`

#### Bad

```javascript
components/
|- MyButton.vue
|- VueTable.vue
|- Icon.vue
```

#### Good

```javascript
components/
|- BaseButton.vue
|- BaseTable.vue
|- BaseIcon.vue
```

#### or

```
components/
|- AppButton.vue
|- AppTable.vue
|- AppIcon.vue
```

### Coupled components

#### Bad

```javascript
components/
|- SearchSidebar.vue
|- NavigationForSearchSidebar.vue
```

#### Good

```javascript
components/
|- SearchSidebar.vue
|- SearchSidebarNavigation.vue
```

### Order of words in component names

#### Bad

```javascript
components/
|- ClearSearchButton.vue
|- ExcludeFromSearchInput.vue
|- LaunchOnStartupCheckbox.vue
|- RunSearchButton.vue
|- SearchInput.vue
|- TermsCheckbox.vue
```

#### Good

```javascript
components/
|- SearchButtonClear.vue
|- SearchButtonRun.vue
|- SearchInputQuery.vue
|- SearchInputExcludeGlob.vue
|- SettingsCheckboxTerms.vue
|- SettingsCheckboxLaunchOnStartup.vue
```

### Closing components

#### Bad

```html
<!-- In single-file components, string templates, and JSX -->
<MyComponent></MyComponent>
```

#### or

```html
<!-- In DOM templates -->
<my-component />
```

#### Good

```html
<!-- In single-file components, string templates, and JSX -->
<MyComponent />
```

#### or

```html
<!-- In DOM templates -->
<my-component></my-component>
```

### Component name casing template

#### Bad

```html
<!-- In single-file components and string templates -->
<mycomponent />
```

```html
<!-- In single-file components and string templates -->
<myComponent />
```

```html
<!-- In DOM templates -->
<MyComponent></MyComponent>
```

#### Good

```html
<!-- In single-file components and string templates -->
<MyComponent />
```

```html
<!-- In DOM templates -->
<my-component></my-component>
```

### Full word Component name

#### Bad

```
components/
|- SdSettings.vue
|- UProfOpts.vue
```

#### Good

```
components/
|- StudentDashboardSettings.vue
|- UserProfileOptions.vue
```

## Folders

**Your folders must always be in lower case, except for folders that represent a component**

#### Bad

```
Pages/
|- articlePages/
   |-- articlePages.vue
   |-- articleTitle.vue
   |-- lastArticlesSection.vue
   |-- index.ts
   |-- style.scss
```

#### Good

```
pages/
|- ArticlePages/
   |-- ArticleTitle.vue
   |-- LastArticlesSection.vue
   |-- index.ts
   |-- style.scss
```
