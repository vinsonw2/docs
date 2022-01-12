# Options: Rendering

## template

A string template for the component instance.

- **Type:** `string`

- **Details**

  Template provided via the `template` option will be compiled on-the-fly, therefore it is only supported when using the full build (i.e. the standalone `vue.js` that can compile templates in the browser).

  The template will **replace** the `innerHTML` of mounted element. Any existing markup inside the mounted element will be ignored.

  If the string starts with `#` it will be used as a `querySelector` and use the selected element's `innerHTML` as the template string. This allows the source template to be authored using native `<template>` elements.

  If the `render` is also present in the same component, `template` will be ignored.

  :::warning Security Note
  Only use template sources that you can trust. Do not use user-provided content as your template. See [Security Guide](/guide/best-practices/security.html#rule-no-1-never-use-non-trusted-templates) for more details.
  :::

## render

A function that programmatically returns the virtual DOM tree of the component.

- **Type**

  ```ts
  interface ComponentOptions {
    render(this: ComponentPublicInstance) => VNodeChild
  }

  type VNodeChild = VNodeChildAtom | VNodeArrayChildren

  type VNodeChildAtom =
    | VNode
    | string
    | number
    | boolean
    | null
    | undefined
    | void

  type VNodeArrayChildren = (VNodeArrayChildren | VNodeChildAtom)[]
  ```

- **Details:**

  `render` is an alternative to string templates that allows you to leverage the full programmatic power of JavaScript to declare the render output of the component.

  Pre-compiled templates, for example those in Single-File Components, are compiled into the `render` option at build time. If both `render` and `template` are present in a component, `render` will take higher priority.

- **See also:**
  - [Rendering Mechanism](/guide/extras/rendering-mechanism.html)
  - [Render Functions](/guide/extras/render-function.html)

## compilerOptions

Configure runtime compiler options for the component's template.

This config option is only respected when using the full build (i.e. the standalone `vue.js` that can compile templates in the browser). It supports the same options as the app-level [app.config.compilerOptions](/api/application.html#app-config-compileroptions), and has higher priority for the current component.

- **See also:** [app.config.compilerOptions](/api/application.html#app-config-compileroptions)