# gatsby-remark-reading-time

Adds a medium-like reading time estimate to your Gatsby remark posts. Powered by [`reading-time`](https://github.com/ngryman/reading-time).

This plugin supports both **MD** and **MDX** formats.

## Installation

Install

```bash
yarn add gatsby-remark-reading-time
```

### Markdown (MD)

Add to `gatsby-transformer-remark` plugins in `gatsby-config.js`

```js
// gatsby-config.js
  ...
  plugins: [
    ...
    {
      resolve: `gatsby-transformer-remark`,
      options: {
        plugins: [
          `gatsby-remark-reading-time`,
          // ...
        ],
      },
    },
  ]
```

### MDX

Add this plugin outside your `gatsby-plugin-mdx` config, i.e. this plugin should not live within either of `remarkPlugins` or `gatsbyRemarkPlugins` config options:

```js
// gatsby-config.js
  ...
  plugins: [
    {
      resolve: `gatsby-plugin-mdx`,
      options: {
        gatsbyRemarkPlugins: [...],
        remarkPlugins: [...],
      },
    },
    'gatsby-remark-reading-time',
     ...
  ],
```

## Usage

The reading time can be queried in the relevant markdown fields. An example of this is shown below for a single post:

### Markdown (MD)

If you are using the `gatsby-transformer-remark` plugin then you can use:

```jsx
export const query = graphql`
  query($slug: String!) {
    markdownRemark(fields: { slug: { eq: $slug } }) {
      htmlAst
      excerpt(pruneLength: 200)
      frontmatter {
        title
        date(formatString: "MMMM Do, YYYY")
      }
      fields {
        slug
        readingTime {
          text
        }
      }
    }
  }
`;
```

### MDX

If you are using the `gatsby-plugin-mdx` plugin then you can use:

```jsx
export const query = graphql`
  query($slug: String!) {
    mdx(fields: { slug: { eq: $slug } }) {
      body
      excerpt(pruneLength: 160)
      frontmatter {
        title
        date(formatString: "MMMM Do, YYYY")
      }
      fields {
        readingTime {
          text
        }
      }
    }
  }
`;
```

### Fields

There are 4 available fields within `readingTime`:

- `text`: '1 min read',
- `minutes`: 1,
- `time`: 60000, (_milliseconds_)
- `words`: 200

## License

MIT
