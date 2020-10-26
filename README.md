# rehype-all-the-thumbs

> rehype-👍🏿👍🏼👍🏽👍🏻👍🏾

[`rehype-all-the-thumbs`](https://github.com/ericdmoore/rehype-all-the-thumbs) is a unifiedjs/rehypejs plugin that finds images in your DOM, and makes thumbnail images automatically. It also ships with defaults so you can get started with no config and get reaasonable results, and it also offers extensive config options to meet various needs.


![Readme Diagram](pics/Readme-diagram.svg)

`rehype-all-the-thumbs` comes with:
- a default config
- options to set a user default in the unified processor
- options to set configuration for each node in the DOM individullly
- options on where to save/emit these images.

## Behind the Scenes 

`rehype-all-the-thumbs` is actually a unified preset that composes smaller plugins together... and those other plugins are available for develoeprs should you have a need similar to the solution those aim to solve.

The Following are Nominated for Best Supporting Plugins in RehypeAllTheTumbs:

- [rehype-all-the-thumbs-curate](https://github.com/ericdmoore/rehype-all-the-thumbs-curate) (DOM -> data.srcs)
- [rehype-all-the-thumbs-create](https://github.com/ericdmoore/rehype-all-the-thumbs-create) (data.srcs -> data.newAssets)
- [rehype-all-the-thumbs-manipulate](https://github.com/ericdmoore/rehype-all-the-thumbs-manipulate) (data.newAssets -> DOM)
- [rehype-all-the-thumbs-obviate](https://github.com/ericdmoore/rehype-all-the-thumbs-obviate) (data.newAssets.filter -> data.newAssets)
- [vfile-newAssets-generate](https://github.com/ericdmoore/vfile-newAssets-generate) (data.newAssets -> Side Effect Funtion to create the file)



## Simple Usage

```js
const path = require('path')
const parse = require('rehype-parse')
const makeThumbs = require('rehype-all-the-thumbs')
const stringify = require('rehype-stringify')

const write = (vf, i arr, next)=>{
    const base = '/public'
    fs.createFile(path.resolve(base, vf.path), vf.contents, (err)=>{
        err ? next(err) : next(null, true)
    })
}

unified()
.use(parse)
.use(makeThumbs, {write})
.use(stringify)
```



## Full Monty Usage

```js
const path = require('path')
const parse = require('rehype-parse')
const makeThumbs = require('rehype-all-the-thumbs')
const stringify = require('rehype-stringify')

const read = (path, next)=>{
    const base = '/public'
    fs.readFile(path.resolve(base, path), (err, data)=>{
        // cb( Error?, alreadyExists )
        err ? cb(err, true) : cb(null, false)
    })
}
const write = (vf, i arr, next)=>{
    const base = '/public'
    fs.createFile(path.resolve(base, vf.path), vf.contents, (err)=>{
        err ? next(err) : next(null, true)
    })
}
const select = 'picture img[thumbnails="true"]'
const widths = [100, 250, 450, 600] 
const breaks = [640, 980, 1020]
const types = {webp:{}, jpg:{}} // where the empty object implies use the default for the format
const prefix = 'optim/'
const className = undefined
const suffix = '-{{width}}w-{{hash}}.{{ext}}'


unified()
.use(parse)
.use(makeThumbs, {select, hashLen:8, widths, breaks, types, classNames, prefix, suffix, read, write})
.use(stringify)
```

### Using a simple configuration

#### input file 

```html
<!doctype>
<html>
  <head>
    <title>Exmaple HTML</title>
  </head>
  <body>
    <h1>HTML W/ a Picture to Parse</h1>
    <picture thumbnails="true">
        <img alt="A Lovely Description" src="/images/example.jpg" />
    </picture>
  <body>
</html>
```


#### Output file

```html
<!doctype>
<html>
  <head>
    <title>Exmaple HTML</title>
  </head>
  <body>
    <h1>HTML W/ a Picture to Parse</h1>
    <picture thumbnails="true" data-widths="[500, 750]" data-breaks="[800]" data-formats="webp,jpg">
        <source 
            type="image/webp" media="(min-width: 801px)"
            srcset="/optim/images/example-750w-D463ABBA.webp" />
        <source 
            type="image/jpeg" media="(min-width: 801px)"
            srcset="/optim/images/example-750w-AB3DA4C1.jpg" />
        <source 
            type="image/webp" media="(max-width: 800px)"
            srcset="/optim/images/example-500w-2A957B2E.webp" />
        <source 
            type="image/jpeg" media="(max-width: 800px)"
            srcset="/optim/images/example-500w-129FD583.jpg" />
        <img alt="A Lovely Description" src="/images/example.jpg"/>
    </picture>
  <body>
</html>
```

#### Other Output Files
Additionally, 4 new images are created on the file system:

- `/optim/images/example-750w-D463ABBA.webp`
- `/optim/images/example-750w-AB3DA4C1.jpg`
- `/optim/images/example-500w-2A957B2E.webp`
- `/optim/images/example-500w-129FD583.jpg`

## Clarification

If you are using one of the "...ate" plugins, and you are not making a preset, or developing other plugins, if you "Just  want some thumbnails to show up", you should jump up one level and use the main plugin `rehype-all-the-thumbs`

> rehype-👍🏿👍🏼👍🏽👍🏻👍🏾 (main plugin)

## License

[MIT][license] © [Eric D Moore][author]

<!-- Definitions -->

[license]: LICENSE

[author]: https://im.ericdmoore.com
