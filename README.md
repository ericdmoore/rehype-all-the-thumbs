# rehype-all-the-thumbs

> rehype-👍🏻👍🏼👍🏽👍🏾👍🏿
> a love child of rehypejs and sharp image processing (main plugin)

`rehype-all-the-thumbs` is a unifiedjs plugin that will find images in your DOM, and make thumbnail images automatically.

Ships with defaults so no config is required but offers extensive config options to meet various needs.

`rehype-all-the-thumbs` is made up of other plugins that can be used by other develoeprs if it meets your needs.

`rehype-all-the-thumbs` comes with:
- a default config
- options to set a user default in the unified processor
- options to set configuration for each node in the DOM individullly
- options on where to save/emit these images.

Uses Plugins:

- [rehype-all-the-thumbs-curate](https://github.com/ericdmoore/rehype-all-the-thumbs-curate) (DOM -> data.srcs)
- [rehype-all-the-thumbs-create](https://github.com/ericdmoore/rehype-all-the-thumbs-create) (data.srcs -> data.newAssets)
- [rehype-all-the-thumbs-manipulate](https://github.com/ericdmoore/rehype-all-the-thumbs-manipulate) (data.newAssets -> DOM)
- [rehype-all-the-thumbs-obviate](https://github.com/ericdmoore/rehype-all-the-thumbs-obviate) (data.newAssets.filter -> data.newAssets)
- [vfile-newAssets-generate](https://github.com/ericdmoore/vfile-newAssets-generate) (data.newAssets -> Side Effect Funtion to create the file)

So if you are using on of the ...ate plugins and you just want some thumbnails to show up, you should jump up one level and use the main plugin `rehype-all-the-thumbs`

> rehype-👍🏻👍🏼👍🏽👍🏾👍🏿
