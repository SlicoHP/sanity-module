---
title: Files
description: 'Access text, images, and other media with Nuxt and the Sanity headless CMS.'
category: Helpers
position: 12
version: 0.80
---

## Global helper

This module defines a global `<SanityFile>` component to assist with auto-generating your file URLs. It is a lightweight functional component that simply turns the props into a valid file URL.

### Props

#### `assetId`

The Sanity asset ID (of the form `file-41773b5c55bc5414ab7554a75eefddf8e2e14524-txt`).

- Type: **string**
- **Required**

#### `projectId` and `dataset`

These default to the `projectId` and `dataset` passed into the module options but can be overridden.

- Type: **string**

#### `download`

- Type: **string** or **boolean**
- Default: `false`

If set, the URL will contain a download link to that asset. If set to a string, the file will download to that filename. Otherwise, the original filename will be used (if saved in Sanity). If the original filename is not available, the id of the file will be used instead. See [the Sanity documentation](https://www.sanity.io/docs/file-type).

### Example

```vue
<template>
  <SanityFile asset-id="file-41773b5c55bc5414ab7554a75eefddf8e2e14524-txt">
    <template #default="{ src }">
      <a :href="src">Click here to read this text file</a>
    </template>
  </SanityFile>
</template>
```

## Local import

You may wish to import `SanityFile` only in the components that need it, if you have disabled the global `imageHelper` option.

### Example

```vue
<template>
  <SanityFile asset-id="file-41773b5c55bc5414ab7554a75eefddf8e2e14524-txt" download="myfile.txt">
    <template #default="{ src }">
      <a :href="src">Click here to download</a>
    </template>
  </SanityFile>
</template>

<script>
import { SanityFile } from '@nuxtjs/sanity/dist/components/sanity-file'

export default {
  components: { SanityFile },
}
</script>
```
