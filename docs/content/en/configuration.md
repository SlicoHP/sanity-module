---
title: Configuration
description: 'Access text, images, and other media with Nuxt and the Sanity headless CMS.'
category: Getting started
position: 3
version: 0.31
---

By default, `@nuxtjs/sanity` will look for a `sanity.json` file in your project root directory, and it will read your `projectId` and `dataset` from there.

```json{}[sanity.json]
{
  "api": {
    "projectId": "sample-project-id",
    "dataset": "production"
  }
}
```

If you need to provide additional configuration, you can pass in an object in your Nuxt config with key details:

```js{}[nuxt.config.js]
{
  sanity: {
    projectId: 'myProject',
  },
}
```

## Runtime configuration

It is also possible to pass options to this module through [runtime configuration](https://nuxtjs.org/guide/runtime-config/), via a `sanity` key. If you do so they will be merged with (and override) any other options passed in.

For example:

```js{}[nuxt.config.js]
{
  privateRuntimeConfig: {
    sanity: {
      token: process.env.SANITY_TOKEN,
    },
  },
  sanity: {
    projectId: 'myProject',
  },
}
```

## Reference

### `projectId`

- **Required**
- Type: **string**

Your Sanity Project ID, which you can find in your Sanity dashboard.

![](/sanity-dashboard.png)

### `dataset`

- Type: **string**
- Default: **`'production'`**

### `token`

- Type: **string**

You can provide a token or leave blank to be an anonymous user. (You can also set a token programmatically in a Nuxt plugin.)

### `withCredentials`

- Type: **boolean**
- Default: **`false`**

Include credentials in requests made to Sanity. Useful if you want to take advantage of an existing authorisation to the Sanity CMS.

### `useCdn`

- Type: **boolean**
- Default: **`true`** in production or **`false`** if a token has been passed in

### `minimal`

- Type: **boolean**
- Default: **`false`**

Use an ultra-minimal Sanity client for making requests (a fork of [picosanity](https://github.com/rexxars/picosanity) with SSR-specific changes). It only supports `fetch` requests, but will significantly decrease your bundle size.

<d-alert type="info">If you don't have `@sanity/client` installed, then `@nuxtjs/sanity` will use the minimal client by default.</d-alert>

### `imageHelper`

- Type: **boolean**
- Default: **`true`**

Add a global `<SanityImage>` component to assist with URL transformations. See [the docs](/helpers/images) for more information.

If you have `components: true` set in your `nuxt.config` file, then this option has no effect and this helper will be registered with `@nuxt/components` and imported only where needed, rather than registered globally.

### `contentHelper`

- Type: **boolean**
- Default: **`true`**

Add a global `<SanityContent>` component to display portable text. See [the docs](/helpers/portable-text) for more information.

If you have `components: true` set in your `nuxt.config` file, then this option has no effect and this helper will be registered with `@nuxt/components` and imported only where needed, rather than registered globally.

### `disableSmartCdn`

- Type: **boolean**
- Default: **`false`**

By default, if [Preview Mode](https://nuxtjs.org/docs/2.x/features/live-preview) has been switched on, `useCdn` will be disabled. If this behaviour isn't desirable, you can disable it by setting `{ disableSmartCdn: false }`.

### `additionalClients`

- Type: **Object**
- Default: **`{}`**

You can create additional clients. Each client's name will be the key of the object provided, and the options provided will be merged with the options of the default client.

The options that can be provided are:

- `projectId`
- `dataset`
- `token`
- `withCredentials`
- `useCdn`

So, for example:

```js{}[nuxt.config.js]
{
  // ...
  sanity: {
    additionalClients: {
      another: {
        projectId: 'anotherproject',
      },
    },
  },
}
```

<d-alert>Because these clients will be accessible directly off the `$sanity` helper, take care not to name them `client`, `fetch` or `setToken`, or they will conflict with the default client properties.

</d-alert>
