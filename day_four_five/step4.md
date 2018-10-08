# Posts Component

When we make a GET request to `/posts` through our `DataSource` object, we get back an array of objects, which looks like this:

```js
[{
  id: 102,
  userId: 1,
  title: "my post",
  body: "woooo"
}, {
  id: 103,
  userId: 1,
  title: "another post",
  body: "ok ok ok"
}, {
  id: 104,
  userId: 2,
  title: "my trip to the seaside",
  body: "got bit by a crab"
}]
```

The `Posts` component will take this data and [map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) over it, replacing each element with the output of calling our `Post` component on each element - in other words, an array of HTML strings. The `Posts` method should then [join](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join) this array of HTML strings together to create a single HTML string that can be passed to `DOM.prototype.render()`.

Have a go at creating this on your own, then compare to our solution below.

<details>
  <summary>Spoiler</summary>

  ```js
  function Posts (posts) {
    const postElements = posts.map(function (post) {
      return Post(post);
    });

    return postElements.join('');
  }
  ```

</details>

## Try it out

In your `index.html` file, include in the component file. Inside your `DOM` instance's `render` method (create a new instance if you deleted your practice code from earlier), call the `Posts` component function, passing in the following object:

```js
[{
  id: 102,
  userId: 1,
  title: "my post",
  body: "woooo"
}, {
  id: 103,
  userId: 1,
  title: "another post",
  body: "ok ok ok"
}, {
  id: 104,
  userId: 2,
  title: "my trip to the seaside",
  body: "got bit by a crab"
}]
```

You should see the posts outputted to your `div#root` element.

***
:exclamation:
You will need to ensure that you import the `Posts.js` file into your `index.html` file **after** `Post.js`, as `Posts` relies on the `Post` method already being in memory, and JavaScript is procedural - that is, it runs line by line.
***

## [Step 5: Challenge: Displaying Posts](step5.md)
