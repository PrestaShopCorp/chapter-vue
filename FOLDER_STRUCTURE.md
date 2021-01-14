# Folder structure

## Module-based, not file-based structure

When starting a new Vue project, the easiest way to go is vue-cli project structure, which somehow forces you to group your files by type: components, services, helpers with a few odd exceptions, such as the router and the store. This structure is not wrong — for small applications, it’s very easy to maintain, but for mid-size/large applications there are a few downsides:

- The source code navigation is not simple: imagine the amount of files inside the components folder, and knowing the purpose of each one — same for any other file type
- Debugging can be very time-consuming: you’d need to jump file-to-file and draw a mental map of how a simple process works to get to the root cause of a bug

A better alternative is to structure your project using old-fashioned modules and to think of each module as a small vue-cli project, decreasing the downsides explained above, so you get something like this:

```javascript
src/
+-- modules/
|   +-- moduleA/
|       +-- components/
|       +-- services/
|       +-- helpers/
|       +-- router/
|       +-- store/
|   +-- moduleB/
|   +-- moduleC/
```

You’ll end up with very few files per folder, as every file inside a module should only contribute to the module responsibilities, and if you still have too many files, consider splitting into smaller modules.
This improved cohesion will make the source code navigation, debugging and general maintainability easier.

## Isolate your module

Having a modular system usually implies having interaction between the different components in the system, and that’s why isolating the modules as much as possible is so important. Isolating modules means having a) strong encapsulation so implementation details are hidden, b) well-defined module API to limit and control the interactions and c) explicit dependencies to verify the modules’ construction.
These principles allow teams to collaborate on large projects independently, with the confidence of not breaking other components in the system — but how do you achieve this in Vue?
Explicit module objects: we need a way to declare a module with its dependencies and initialisation, and a JavaScript object or a class can help with this:

```javascript
export class MyModule {
  constructor(store, router) {
    this.store = store;
    this.router = router;
  }

  install(options = {}) {
    // Initialise the module using dependencies
  }
}
```

And if you do this using TypeScript, you could enforce dependency and interfaces at compilation time.

**Register Vuex store module dynamically** with registerModule method. This can be done either in the module constructor or initialisation method.
**Add routes dynamically** with addRoutes method. VueRouter doesn’t currently support add child routes to an existing parent so, unless you want to use another library to make this happen, you’ll probably need to design your router tree based on your modules, so they get their own branch from the root, e.g, /products/_ belongs to products module, /checkout/_ belongs to payments module, and so on.

**Install modules on the app’s initialisation**, e.g. in main.(js|ts):

```javascript
import Vue from 'vue'
import { StoreModule } from '@/modules/store'
import { RouterModule } from '@/modules/router'
import { ProductsModule } from '@/modules/products'
function bootstrap() {
  const storeModule = new StoreModule()
  const routerModule = new RouterModule()
  const productsModule = new ProductsModule(
    storeModule.store,
    routerModule.router
  )
  productsModule.install()
  ...

  new Vue({ ... })
}
bootstrap()
```

## Group modules according to your business

There are two kinds of modules:

- Core Modules: contribute to the app’s core functionalities such as store, router, translations, etc
- Feature Modules: add support to the different features the app provides to users, e.g. product list and details, checkout, user settings, etc

Grouping the latter (Feature modules) according to your business, i.e. the features provided to your users, provides the following benefits:

- A business request will change the least amount of modules because the modules are responsible for whole features from the user experience perspective
- Observability and monitoring can be improved by tagging the reports by module. This can make it easier to assign tickets to the responsible team
- Integration/acceptance tests can be limited to the module responsibilities

## Use README.md to give context

Technical documentation is very important for large projects where it’s easy to get lost. A simple but very effective tool is the README.md file in the root of each module.
In this file, you can provide a very simple context to readers, such as:

1. Module responsibilities
2. Exported functionality (services, helpers, components, etc)
3. Dependencies
4. Any extra important context, like important internal services
