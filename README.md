# metalsmith-tags-list

  A metalsmith plugin to create dedicated pages for tags in provided in metalsmith pages.

## Installation

    $ npm install metalsmith-tags-list

## Description in Pages

  In your pages:

```
---
title: This is page with tags
tags: tagged, page, metalsmith, plugin
---

Hello World
```

Then split the string data in the field using metalsmith-metadata-as-list. 

You can use different handle for the tags, by configuring the `handle` option. `tags` is the default.


## CLI Usage

  Install the node modules and then add the `metalsmith-tags` key to your `metalsmith.json` plugins. The simplest use case just requires tag handle you want to use:

```json
{
  "plugins": {
    "metalsmith-tags-list": {
      "handle": "tags",
      "path": "topics/:tag.html",
      "template": "/partials/tag.hbt",
      "sortBy": "date",
      "reverse": true
    }
  }
}
```

## JavaScript Usage

  Pass the plugin to `Metalsmith#use`:

```js
var tags = require('metalsmith-tags-list');

metalsmith
    .use(tags({
        handle: 'tags',                  // yaml key for tag list in you pages
        path:'topics/:tag.html',                   // path for result pages
        template:'/partials/tag.hbt',    // template to use for tag listing
        sortBy: 'date',                  // provide posts sorted by 'date' (optional)
        reverse: true                    // sort direction (optional)
    }));
```

## Result

  This will generate `topics/[tagname].html` pages in your `build` directory with array of `pagination.files` objects on which you can iterate on. You can use `tag` for tag name in your templates. (You can refer to tests folder for tags template.)

  You can use `metalsmith-permalink` to customize the permalink of the tag pages as you would do with anything else.

  It is possible to use `opts.metadataKey` for defining the name of the global tag list.
  By default it is `'tags'`.

## Pagination

  Additionally you can paginate your tag pages.  To do so add two additional properties to your configuration object, `pathPage` and `perPage`, and modify `path` to point to the root pagination location:

```json
{
  "handle": "tags",
  "path": "topics/:tag/index.html",
  "pathPage": "topics/:tag/:num/index.html",
  "perPage": 6,
  "template": "/partials/tag.hbt",
  "sortBy": "date",
  "reverse": true
}
```

  This will paginate your array of tags so that 6 appear per page, with additional tag pages being nested underneath the first page of tags.  For additional details please look at the tests.

## Contribution

  Feel free to contribute to this plug-in. Fork, commit, send pull request.
  Issues, suggestions and bugs are more than welcome.

  In case you add functionality, please write corresponding test. Test using `npm test`.

  hrehf: Sorry, I didn't.

  Thanks!

## License

  MIT
