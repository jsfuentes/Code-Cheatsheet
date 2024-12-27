# Data Integrations

Can be done without [GraphQL](https://www.gatsbyjs.org/docs/using-gatsby-without-graphql/)

Use source plugins to get data from filesystem etc, then use transformer(transformer page) to 

Checkout http://localhost:8000/___graphql for graphql interface

## Pulling Data

### Page Queries

live outside of the component definition — by convention at the end of a page component file — and are only available on page components.

gatsby-config.js

```js
module.exports = {
  siteMetadata: {
    title: `Title from siteMetadata`,
  }
}
```

src/pages/about.js

```js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"

export default ({ data }) => (
  <Layout>
    <h1>About {data.site.siteMetadata.title}</h1> 
    <p>
      We're the only site running on your computer dedicated to showing the best
      photos and videos of pandas eating lots of food.
    </p>
  </Layout>
)

export const query = graphql`
  query {
    site {
      siteMetadata {
        title
      }
    }
  }
```

### Static Query

Allows non-page components (`layout.js`), to get data

```js
import React from "react"
import { useStaticQuery, graphql } from "gatsby"

export default ({ children }) => {
  const data = useStaticQuery(
    graphql`
      query {
        site {
          siteMetadata {
            title
          }
        }
      }
    `
  )
  
  return (
    <div>
      <h3>
     	 {data.site.siteMetadata.title} 
      </h3>
      {children}
    </div>
  )
}
```

## Source Plugins

fetch data from sources like: Wordpress

#### File System

[`gatsby-source-filesystem`](https://www.gatsbyjs.org/packages/gatsby-source-filesystem/)  basically gets you all local files in your gatsby folder with `allFile` and `file` query 

```js
  plugins: [
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `src`,
        path: `${__dirname}/src/`,
      },
    },
```

```js
import React from "react"
import { graphql } from "gatsby"

export default ({ data }) => {
  return (
      <div>
        <h1>My Site's Files</h1>
        <table>
          <thead>
            <tr>
              <th>relativePath</th>
              <th>prettySize</th>
              <th>extension</th>
              <th>birthTime</th>
            </tr>
          </thead>
          <tbody>
            {data.allFile.edges.map(({ node }, index) => (
              <tr key={index}>
                <td>{node.relativePath}</td>
                <td>{node.prettySize}</td>
                <td>{node.extension}</td>
                <td>{node.birthTime}</td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
	)
}

//Recall json shape is like the query
export const query = graphql`
  query {
    allFile {
      edges {
        node {
          relativePath
          prettySize
          extension
          birthTime(fromNow: true)
        }
      }
    }
  }
`
```