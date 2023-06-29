## Configuration

To configure FormKit create a `formkit.config.js` in the root of your Nuxt project. The provided Nuxt module automatically uses the `formkit.config.js` that is at the root of your project to extend FormKit's functionality. Your config file should export a [configuration object](/essentials/configuration#what-is-defaultconfig).

### formkit.config.js
```js
import { fr } from '@formkit/i18n'

export default {
  locales: { fr },
  locale: 'fr',
}
```

### Using environment variables in formkit.config.js

There may be instances where you want to use Nuxt's `runtimeConfig` variables inside of your `formkit.config.js` file — such as keeping a FormKit Pro API key from being published in your codebase. To achieve this you can provie a function to `defineFormKitConfig` which returns a configuration object. Your function will be called by Nuxt and have access to `runtimeConfig`.

```js
import { fr } from '@formkit/i18n'
import { defineFormKitConfig } from '@formkit/vue'
import { createProPlugin, inputs } from '@formkit/pro'

export default defineFormKitConfig(() => {
  // here we can access `useRuntimeConfig` because
  // our function will be called by Nuxt.
  const config = useRuntimeConfig()

  // and we can use the variables to import secrets
  const pro = createProPlugin(config.FORMKIT_PRO_KEY, inputs)

  return {
    plugins: [pro],
    locales: { fr },
    locale: 'fr',
  }
})
```

### Defining a custom FormKit config path

If you would like to supply a custom path to your `formkit.config`, you can override the default location using the `configFile` option under the `formkit` key. **Any path you supply should be relative to the root of your Nuxt project**:

```js
// nuxt.config
export default defineNuxtConfig({
  modules: ['@formkit/nuxt'],
  formkit: {
    configFile: './my-configs/formkit.config.js',
  },
})
```

### Without extending `defaultConfig`

By default, your configuration will _extend_ the `defaultConfig` that ships with FormKit. This is the desired behavior
for the majority of projects. However, if you need to define the entire FormKit config yourself — from scratch — you may do so
by setting the `defaultConfig` option for the module to `false`:

```js
// nuxt.config
export default defineNuxtConfig({
  modules: ['@formkit/nuxt'],
  formkit: {
    defaultConfig: false,
    configFile: './my-configs/formkit.config.js',
    // ^ this is now a full config replacement, not override.
  },
})
```