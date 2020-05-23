[Video Link](https://egghead.io/lessons/gatsby-set-up-yarn-workspaces-for-gatsby-theme-development)

## Summary

In this lesson, we learn how to structure folders and configure Yarn workspaces to make the development of Gatsby themes easier.

## Notes

---

### ⚡ Setting Up Directories

In an empty directory, we create a `package.json`. We set `private` to `true` and `workspaces` to a list of folder names (packages) that we're going to create.

Setting the `private` property prevents your package from being published on npm.

#### root package.json

```json
{
  "private": true,
  "workspaces": ["gatsby-theme-events", "site"]
}
```

Next we'll create new folders for our packages. Each directory will have its' own `package.json`, and the directory names will match the names in the workspaces list we just created.

The first one is called `gatsby-theme-events`. We set the `name`, `version`, and `licence` properties.

Because this will be installed as a package, we also need to set the `main` property. This is the entry point to your project.

#### gatsby-theme-events/package.json

```json
{
  "name": "gatsby-theme-events",
  "version": "1.0.0",
  "license": "MIT",
  "main": "index.js"
}
```

Next we'll create `gatsby-theme-events/index.js` and leave it empty except for a comment.

#### gatsby-theme-events/index.js

```js
// this file is empty!
```

In `site/package.json`, we set `private` to `true` because we are not going to publish this site as a npm package.

We add a `name`, `version` and `licence` property just as before along with `scripts`.

#### site/package.json

```json
{
  "private": true,
  "name": "site",
  "version": "1.0.0",
  "license": "MIT",
  "scripts": {
    "build": "gatsby build",
    "clean": "gatsby clean",
    "develop": "gatsby develop"
  }
}
```

We also want to add `scripts` to our theme site, so we copy and paste it over.

#### gatsby-theme-events/package.json

```json
{
  ...
  "main": "index.js",
  "scripts": {
    "build": "gatsby build",
    "clean": "gatsby clean",
    "develop": "gatsby develop"
  }
}
```

### ⚡ Installing Workspace Dependencies

Next we install our dependencies. Instead of using `yarn add`, we use `yarn workspace <workspace name> add`.

We will add Gatsby, React, ReactDOM and our theme, `gatsby-theme-events`

```bash
$ yarn workspace site add gatsby react react-dom gatsby-theme-events@*
```

We use the '@\*' because we are adding an unpublished theme.

If we run `yarn workspaces info` we can see that the `site` is using `gatsby-theme-events` from our workspace. 🎉

Our theme also needs to have Gatsby, React and ReactDOM added as peer dependencies.

```bash
$ yarn workspace gatsby-theme-events add -P react react-dom gatsby
```

The `-P` flag tells Yarn to add these packages as peer dependencies.

During development we are going to use our theme as a regular Gatsby site, so we'll add the previous packages as dev dependencies.

```bash
$ yarn workspace gatsby-theme-events add -D react react-dom gatsby
```

### ⚡ Starting the Development Servers

To make sure everything is working correctly, we can start up a dev server for our site.

```bash
$ yarn workspace site develop
```

There are currently no pages set up, so we will see a `404` page.

We also want to check if our theme site is working, so we'll start up another dev server.

```bash
$ yarn workspace gatsby-theme-events develop
```

We should see another `404` page.

## Additional Resources

---

- [npm docs: private](https://docs.npmjs.com/files/package.json#private)

- [npm docs: main](https://docs.npmjs.com/files/package.json#main)

- [Yarn workspaces](https://classic.yarnpkg.com/en/docs/workspaces/)
