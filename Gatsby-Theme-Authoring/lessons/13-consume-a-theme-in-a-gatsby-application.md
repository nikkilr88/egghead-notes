[Video Link](https://egghead.io/lessons/gatsby-consume-a-theme-in-a-gatsby-application)

## Summary

In this lesson we learn how to install our theme in a new project and add data to it.

## Notes

### ⚡ Installing the theme in a new project

To use the theme we created, we need to start a new project. We can make a directory called `theme-test`, and we'll cd into it.

```bash
$ mkdir theme-test
$ cd theme-test
```

We'll set up the project using `yarn init -y`, and then we can install the dependencies. We will add React, React DOM, Gatsby and our theme (e.g. @nikkilr88/gatsby-theme-events).

```bash
$ yarn init -y
$ yarn add react react-dom gatsby @<npm_username>/<theme_name>
```

Next, open the project in your code editor, create a `gatsby-config.js` file, and add theme to the `plugins` array.

#### gatsby-config.js

```js
module.exports = {
  plugins: ['@<npm_username>/<theme_name>'],
}
```

Next we want to globally install the Gatsby CLI.

```bash
$ yarn global add gatsby-cli
```

Now we can check to see if it's all working! Make sure you're inside of the `theme-test` directory and run `gatsby develop`

```bash
$ gatsby develop
```

Once it's finished building, go to `localhost:8000`, and you should see your theme.

### ⚡ Adding data

To add data to the theme, create an `events.yml` file inside of the `data` directory and add an event.

#### /data/events.yml

```yml
- name: Party
  location: My House
  start_date: 2020-06-19
  end_date: 2020-06-19
  url: https://devnikki.com
```

Once you go back to the browser, you should see your event on the website.
