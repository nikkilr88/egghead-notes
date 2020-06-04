[Video Link](https://egghead.io/lessons/gatsby-configure-a-gatsby-theme-to-take-options)

## Summary

In this lesson we learn how to pass options to our Gatsby theme.

## Notes

In a Gatsby theme, you can pass options to both the gatsby-config and the gatsby-node files.

### ⚡ Passing options to gatsby-config

First we need to open the gatsby config file and convert the exported object over to a function. Any options passed to the theme will be provided as arguments.

Our function will accept a `contentPath` and a `basePath`. We can set the `gatsby-source-filesystem` path to the `contentPath`.

#### gatsby-theme-events/gatsby-config.js

```js
module.exports = ({ contentPath = 'data', basePath = '/' }) => ({
  plugins: [
    {
      resolve: 'gatsby-source-filesystem',
      options: {
        path: contentPath,
      },
    },
  ],
})
```

### ⚡ Passing options to gatsby-node

In the `gatsby-node` file, options are passed as the second argument to the API hooks.

Here we can set `contentPath` to `options.contentPath`, and set the fallback to 'data'.

#### gatsby-theme-events/gatsby-node.js

```js
exports.onPreBootstrap = ({ reporter }, options) => {
  const contentPath = options.contentPath || 'data'

  if (!fs.existsSync(contentPath)) {
    reporter.info(`creating the ${contentPath} directory`)
    fs.mkdirSync(contentPath)
  }
}
```

We can do the same thing for `createResolvers` and `createPages`.

```js
exports.createResolvers = ({ createResolvers }, options) => {
  const basePath = options.basePath || '/'

  ...
}
```

```js
exports.createPages = async ({ actions, graphql, reporter }, options) => {
  const basePath = options.basePath || '/'

  ...
}
```

To test this out, we need to set up our site to use the theme so we can set some options.

In the site gatsby config### ⚡ Setting up our site
file, we will export a config object and include our theme in the plugins array.

Inisde of the `options` object, we will set `contentPath` to `events` and `basePath` to `/events`.

When we start up the site, an `events` directory and page should get created.

#### site/gatsby-config.js

```js
module.exports = {
  plugins: [
    (resolve: 'gatsby-theme-events'),
    (options: {
      contentPath: 'events',
      basePath: '/events',
    }),
  ],
}
```

### ⚡ Testing everything out

To test everything out run the following command:

```bash
$ yarn workspace site develop
```

Inside of the `site` directory, there should be a newly created `events` folder, and we should be able to naviate to `/events` and view the 'Upcoming Events' page (which is currently empty).

If we copy our events over to this new `events` directory and restart the development server (`yarn workspace site develop`), we will see that 6 new pages have been created and our events page is no longer empty.
