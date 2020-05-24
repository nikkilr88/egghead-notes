[Video Link](https://egghead.io/lessons/gatsby-add-static-data-to-a-gatsby-theme)

## Summary

In this lesson we learn how to make sure the data directory exists so gatsby-source-filesystem doesn't throw an error.

## Notes

### ⚡ The steps

To create pages, we need to create a file called `gatsby-node.js` in the root directory of the theme.

Inside of this file we need to do a few things:

1. **Make sure the data directory exists**

   We need to do this so `gatsby-source-filesystem` doesn't throw an arror.

2. **Define the event type**

   If we don't have any events defined, we should get back an empty array, not an error.

3. **Define resolvers for custom fields**

   We are going to have a custom `slug` field. We want to be able to query this along with all of the other event data.

4. **Query for events and create pages**

### ⚡ Creating the gatsby-node file

#### gatsby-theme-events/gatsby-node.js

To make sure that our data exists we can use `onPreBootstrap` API hook from Gatsby.

We're going to grab `reporter` to log what's going on.

Next we're going to create a varible for the content path and set it to the `data` directory we created earlier.

After that we're going to import the `fs` module. There is no need to install any extra dependencies because it's built into Node. Then we'll use it to check if the content path _doesen't_ exist. If it doesn't well go ahead and create it.

```js
const fs = require('fs')

// Make sure the data directory exists
exports.onPreBootstrap = ({ reporter }) => {
  const contentPath = 'data'

  // Check if the path doesn't exist
  if (!fs.existsSync(contentPath)) {
    reporter.info(`creating the ${contentPath} diretory`)

    // Create path
    fs.makeDirSync(contentPath)
  }
}
```

Now the first thing that will happen when starting up a site using this theme is that it will check if the content directory exists, and if it doesn't it will be created.

## Additional Resources

- [The gatsby-node.js API file](https://www.gatsbyjs.org/docs/api-files-gatsby-node/)

- [Gatsby theme conventions](https://www.gatsbyjs.org/docs/themes/conventions/)

- [Node file system module](https://nodejs.org/api/fs.html)
