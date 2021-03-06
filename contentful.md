# Contentful

[Sign up for a free Contentful account](https://www.contentful.com/sign-up/) with GitHub.

![image](https://github.com/andrewmcodes/notes-wiki/raw/master/images/Tue_Mar_09_2021_1615269268801.png)

Add `gem "contentful"` to Gemfile.

![image](https://github.com/andrewmcodes/notes-wiki/raw/master/images/Tue_Mar_09_2021_1615269414573.png)

![image](https://github.com/andrewmcodes/notes-wiki/raw/master/images/Tue_Mar_09_2021_1615269560180.png)

![image](https://github.com/andrewmcodes/notes-wiki/raw/master/images/Tue_Mar_09_2021_1615269599810.png)

![image](https://github.com/andrewmcodes/notes-wiki/raw/master/images/Tue_Mar_09_2021_1615269618507.png)

![image](https://github.com/andrewmcodes/notes-wiki/raw/master/images/Tue_Mar_09_2021_1615269633762.png)

![image](https://github.com/andrewmcodes/notes-wiki/raw/master/images/Tue_Mar_09_2021_1615269655084.png)

![image](https://github.com/andrewmcodes/notes-wiki/raw/master/images/Tue_Mar_09_2021_1615269671842.png)

![image](https://github.com/andrewmcodes/notes-wiki/raw/master/images/Tue_Mar_09_2021_1615269687051.png)

![image](https://github.com/andrewmcodes/notes-wiki/raw/master/images/Tue_Mar_09_2021_1615269782177.png)

![image](https://github.com/andrewmcodes/notes-wiki/raw/master/images/Tue_Mar_09_2021_1615269975813.png)

```ruby
require 'dotenv/load'

client = Contentful::Client.new(
  space: ENV["CONTENTFUL_SPACE_ID"],
  access_token: ENV["CONTENTFUL_ACCESS_TOKEN"],
  dynamic_entries: :auto
)
```

```
contentful_bootstrap create_space andrewmcodes --template blog
```

Install cloudinary and graphql playground

```
query {
  accountCollection {
    items {
      sys {
        id
        publishedAt
        firstPublishedAt
        publishedVersion
      }
      title
      url
      username
      image {
        title
        url
      }
    }
  }
}

```

```
query {
  pageCollection {
    items {
      title
      description
      content
      sys {
        id
        publishedAt
        publishedVersion
        firstPublishedAt
      }
    }
  }
}
```
