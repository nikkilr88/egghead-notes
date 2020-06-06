[Video Link](https://egghead.io/lessons/gatsby-publish-a-gatsby-theme-to-npm)

## Summary

In this lesson we learn how to publish our Gatsby theme to npm.

## Notes

Before we can publish our theme, we need to make some updates to our `package.json`.

### ⚡ Namespacing

The first thing we want to do is namespace our theme. This helps us keep track of who published it, and it also helps avoid naming collisions.

#### gatsby-theme-events/package.json

```json
{
  "name": "@your_username/gatsby-theme-events"
}
```

### ⚡ Logging into npm

Next we need to make sure we're logged into npm. To do this, run the following command:

```bash
$ npm whoami
```

If we're not logged in, it will throw an error. To log in, run `npm adduser`.

```bash
$ npm adduser
```

You will be propmted for your npm username, password and email. Running the `npm whoami` command again, it should show you your username.

### ⚡ Publishing the theme

Now that everything is set up, we want to change directories into `gatsby-theme-events`.

```bash
$ cd gatsby-theme-events/
```

To publish our theme, we run the `npm publish` command. Because our theme is namespaced, we need to add the `--access public` flag.

```bash
$ npm publish --access public
```

Now you should be able to see your theme on the npm website at `npmjs.com/package/<the name of your theme>`. 🎉

## Additional Resources

- [npm: Contributing packages to the registry](https://docs.npmjs.com/packages-and-modules/contributing-packages-to-the-registry)

- [npm publish (cli command)](https://docs.npmjs.com/cli/publish)
