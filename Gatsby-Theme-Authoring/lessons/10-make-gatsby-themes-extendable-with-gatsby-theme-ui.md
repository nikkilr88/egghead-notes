[Video Link](https://egghead.io/lessons/gatsby-make-gatsby-themes-extendable-with-gatsby-theme-ui)

## Summary

In this lesson we learn how to create a theme.js file and allow people using your theme to apply their own design by defining design tokens with theme-ui.

## Notes

_What `gatsby-theme-ui` does is take a global theme context object and makes it available to all themes._

It is part of a system UI network of tools, which means that it's going to give us an object that follows the system UI theme specification.

### ⚡ Installing `gatsby-theme-ui`

We can make our theme's styles "extendable" with `gatsby-theme-ui`. To install this package and its dependencies, run the following command:

```bash
$ yarn workspace gatsby-theme-events add gatsby-theme-ui theme-ui @emotion/core @emotion/styled @mdx-js/react
```

Once that's done, we can add `gatsby-theme-ui` to the `plugins` array in the theme gatsby config file.

#### gatsby-theme-events/gatsby-config.js

```js
module.exports = ({ contentPath = 'data', basePath = '/' }) => ({
  plugins: [
    'gatsby-theme-ui',
    {
      resolve: 'gatsby-source-filesystem',
      options: {
        path: contentPath,
      },
    },
  ],
})
```

### ⚡ Adding `gatsby-theme-ui` to our project

To use it in our project, we need to make a `theme.js` file in our theme's `src` folder and export a constant called `theme`.

In this file we can set spacing, fonts, colors and even style HTML elements.

#### gatsby-theme-events/src/theme.js

```js
export const theme = {
  // array of different widths set in pixels that we want to provide as padding and margin
  space: [0, 4, 8, 16, 32],
  fonts: {
    body: '-apple-system, BlinkMacSystemFont, Segoe UI, Roboto, sans-serif',
  },
  // array of different font sizes set in pixels
  fontSizes: [16, 18, 20, 22, 27, 36],
  lineHeights: {
    body: 1.45,
    heading: 1.1,
  },
  colors: {
    // Our site uses mostly shades of gray, so here we can set an array of gray colors
    gray: ['#efefef', '#ddd', '#333', '#111'],
    background: '#fff',
    // This is the primary or brand color
    primary: 'rebeccapurple',
  },
  // These are the sizes of our containers, documents, etc.
  sizes: {
    default: '90vw',
    max: '540px',
  },
  // Styles are special because they reference components and markup elements
  styles: {
    // Layout is provided by theme-ui
    Layout: {
      // We will use the third gray color that we set (#333 at index 2) for the layout color
      color: 'gray.2',
      // 'body' is referencing fonts.body that we set above
      fontFamily: 'body',
      // Font size '1' is referencing the font size in the fontSizes array at the first index (18px)
      fontSize: 1,
      lineHeight: 'body',
    },
    // Header is provided by theme-ui
    Header: {
      // We set 'primary' above in colors.primary
      backgroundColor: 'primary',
      // Set in colors.background
      color: 'background',
      fontWeight: 'bold',
      margin: '0 auto',
      // We set 'max' above in sizes.max
      maxWidth: 'max',
      // '3' references the 4th value in our space array. (16px at index 3)
      padding: 3,
      // We set default above in sizes.default
      width: 'default',
      a: {
        color: 'inherit',
      },
    },
    Main: {
      margin: '0 auto',
      maxWidth: 'max',
      width: 'default',
    },
    Container: {
      padding: 3,
    },
    // Here we are styling basic HTML elements
    h1: {
      color: 'gray.3',
      fontSize: 5,
      fontWeight: 'bold',
      lineHeight: 'heading',
      margin: 0',
      marginTop: 3
    },
    ul: {
      borderTop: '1px solid',
      borderColor: 'gray.0',
      listStyle: 'none',
      padding: 0,
    },
    li: {
      borderBottom: '1px solid',
      borderColor: 'gray.1',
      padding: 2,
      // This is to taget pseudo-classes
      // When the user hovers over a li element, we set the background color to the first gray in the colors.gray array
      '&:focus-within,&:hover': {
        backgroundColor: 'gray.0',
      },
    },
  },
}
```

## Additional Resources

- [Theme UI](https://www.gatsbyjs.org/docs/theme-ui/)
