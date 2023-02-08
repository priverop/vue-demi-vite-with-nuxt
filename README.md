# Nuxt Library Consumption Test

I'm trying to create a [Vue-demi](https://github.com/vueuse/vue-demi) components library with [Vite library mode](https://vitejs.dev/guide/build.html#library-mode), to get it working with Nuxt 2 and Nuxt 3.

This repo demonstrates this problem. It contains:

- **vite-test-lib** - A minimal Vite library using Vue-Demi. It is published at: https://www.npmjs.com/package/@dprp-astara/vite-test-lib. It exports two components.
- **nuxt3-lib-consumer** - A minimal Nuxt 3 application. Imports the library. Run `yarn install && yarn dev` or `npm install && npm dev`.
- **nuxt2-lib-consumer** - A minimal Nuxt 2 application. Imports the library. Run `yarn install && yarn dev` or `npm install && npm dev`.

## Errors

After running `yarn install && yarn dev` in both the **lib-consumer** projects it works fine in Nuxt 2 but it doesn't work in Nuxt 3.

nuxt.config.ts
```typescript
export default defineNuxtConfig({
    build: {
        transpile: ['@prp-astara/vite-test-lib'],
    },
})
```

```bash
[Vue warn]: Property "_self" was accessed during render but is not defined on instance.                                                                                                                                                                                13:18:50
[Vue warn]: Unhandled error during execution of render function                                                                                                                                                                                                        13:18:50
  at <Anonymous>
[nitro] [dev] [unhandledRejection] TypeError: Cannot read properties of undefined (reading '_c')                                                                                                                                                                       13:18:50
    at Proxy.$ (/vue-demi-vite-with-nuxt/nuxt3-lib-consumer/node_modules/@prp-astara/vite-test-lib/dist/vite-test-lib.umd.js:1:1163)
    at renderComponentRoot (/vue-demi-vite-with-nuxt/nuxt3-lib-consumer/node_modules/@vue/runtime-core/dist/runtime-core.cjs.js:906:44)                                                                                                       13:18:41
    at renderComponentSubTree (/vue-demi-vite-with-nuxt/nuxt3-lib-consumer/node_modules/@vue/server-renderer/dist/server-renderer.cjs.js:719:51)
    at renderComponentVNode (/vue-demi-vite-with-nuxt/nuxt3-lib-consumer/node_modules/@vue/server-renderer/dist/server-renderer.cjs.js:644:16)
    at Module.ssrRenderComponent (/vue-demi-vite-with-nuxt/nuxt3-lib-consumer/node_modules/@vue/server-renderer/dist/server-renderer.cjs.js:94:12)
    at _sfc_ssrRender (/vue-demi-vite-with-nuxt/nuxt3-lib-consumer/app.vue:23:31)
    at renderComponentSubTree (/vue-demi-vite-with-nuxt/nuxt3-lib-consumer/node_modules/@vue/server-renderer/dist/server-renderer.cjs.js:710:17)
    at renderComponentVNode (/vue-demi-vite-with-nuxt/nuxt3-lib-consumer/node_modules/@vue/server-renderer/dist/server-renderer.cjs.js:644:16)
    at Module.ssrRenderComponent (/vue-demi-vite-with-nuxt/nuxt3-lib-consumer/node_modules/@vue/server-renderer/dist/server-renderer.cjs.js:94:12)
    at default (/vue-demi-vite-with-nuxt/nuxt3-lib-consumer/node_modules/nuxt/dist/app/components/nuxt-root.vue:63:37)
```

This is the exact issue I had when you try to get Vue 2 working in Nuxt 3.