# Displaying Comments

Again, how you solve this step is up to you.

The challenge is, on the individual post page, to retrieve from the API a list of comments associated with the post, and render these underneath the post.

The API endpoint for retrieving comments is `GET /posts/{post.id}/comments`.

Take some time investigating the data returned from this endpoint to see what the structure is, and what data each comment contains.

You will also need to create some new components which return the correct html for displaying the comments.

Remember, we only want to display the comments on the `post.html` page, not on the `index.html` page.

There's nothing on this step which you haven't done in the challenge already, so take your time looking back over the work you've done already if you get stuck.

<details>
  <summary>Spoiler</summary>
First of all, we should look at getting the comment data, so we know what we have to play with, to drive the development of this feature.
  
We do this in the post.html file. After fetching the post data, we need to make a second `GET` request to the comments url:
 
 ```js
  dataSource.get(`/posts/${postId}`, function (post) {
    dataSource.get(`/posts/${postId}/comments`, function(comments) {
      console.log(comments);
      dom.render(Post(post));
    });
  });
  ```
  
  The `console.log` tells us that `comments` is an array with the following structure:
  
```json
{
  "postId": 1,
  "id": 1,
  "name": "id labore ex et quam laborum",
  "email": "Eliseo@gardner.biz",
  "body": "laudantium enim quasi est quidem magnam voluptate ipsam eos"
}
```

We now need to do something with this data. We could pass it into the `Post` component, but then the `Post`s on the `index.html` page would also try to render comments, which we don't want.

An alternate solution would be to make a **layout** component, which we can use to link multiple components together. Create a file `layouts/Post.js` and require this into `post.html`.

In the layout file, add the following code:

```js
function PostPage(post) {
  return `
    ${Post(post)}
  `;
}
```

If you've made a `Header` component previously, you may want to add this in too.

Then in `post.html` substitute `dom.render(Post(post));` for `dom.render(PostPage(post));`

Refresh the page - it should still work, but we now have a more flexible structure to our code.

Next make a `Comment` component and require it in to `post.html`. This will be similar to the `Post` component - it will take a single comment object, and return a html string for that comment:

```js
function Comment(comment) {
  return `
    <div class="comment" id="comment-${comment.id}">
      <p class="comment-body">${comment.body}</p>
      <p class="comment-email">${comment.email}</p>
    </div>
  `;
}
```

Then we create a `Comments` component, similar to `Posts`, which maps over an array of comments and returns a `Comment` component for each one.

In this example, I've also added a `<h4>` header to the component.

```js
function Comments(comments) {
  return `
    <div class="comments">
      <h4>Comments</h4>
      ${comments.map(function(comment) {
        return Comment(comment);
      })}
    </div>
  `;
}
```

The final step is to add this `Comments` component to our `PostPage` layout, and pass in the correct data:

In `layouts/Post.js`:
```js
function PostPage(post, comments) {
  return `
    ${Post(post)}
    ${Comments(comments)}
  `;
}
```

and in `post.html` update `dom.render(PostPage(post));` to `dom.render(PostPage(post, comments));`

:clap:
</details>
