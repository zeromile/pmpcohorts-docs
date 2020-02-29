# Laravel 02 - Route Wildcards #

> **Heads Up:** The terms "slug" and "URI Segment" are interchangeable. But "URI Segment" is the _proper_ or official name, according to me. Don't fight me on this.

WordPress is a framework that makes great use of URL "slugs", the practice of naming the location of a page based on the title of the page. This is great for search indexing and it looks a lot cleaner.

Instead of ->
```
  www.mywebsite.com/page.php?section=products&prodtype=chainsaws&manufacturer=husqvarna&model=445e
```
Or the even more cryptic ->
```
  www.mywebsite.com/index.php?page=prochaihusq445e
```
Slugs give us a URL that feels organized and makes sense to humans->
```
  www.mywebsite.com/products/chainsaws/husqvarna/445e
```

## Route Wildcards ##
Any text that is separated by, or begins and ends with a ```/``` in a URL, is called a URI segment. Example ->

```
www.stuff.com/home/articles/copy-and-paste-is-easy/
```

Laravel can read the contents of those segments using a wildcard in the Route function. it looks like this ->
```
Route::get('/posts/{post}', function ($post) {
    return $post;
  });
```
The wildcard is the ```{post}``` in the above example. This Route, when accessed, would return (echo) to the browser anything that was typed in the URI segment after ```/posts/```.

It works because the wildcard named in the single enclosures is translated to a variable named ```$post``` that we can then pass into the anonymous ```function``` as a parameter. Which, in this case, is simply returned to the browser.

To pass that value along to a view file we would include it in the second parameter array, like this ->

```
Route::get('/posts/{post}', function ($post) {

  return view('post', ['post' => $post]);
});
```
Or, more commonly as ->
```
Route::get('/posts/{post}', function ($post) {

    return view('post', [
      'post' => $post
    ]);
  });
```
> **Fun Fact:** Breaking an array over multiple lines is perfectly acceptable in PHP...as long as we close the array and separate the key/value pairs with commas correctly.

Let's go ahead and create the ```post``` blade file in ```/resources/views/```. In my editor, Atom, I can right click on this folder and choose ```New File```. It will then ask me what to name the file. In this case it should be ```post.blade.php```.

Once the file is created go ahead and add the standard boilerplate HTML and an enclosure to handle the ```post``` array key ->
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>
  {{ $post }}
</body>
</html>
```

Test in your browser. Anything you type after ```/posts/``` should be echoed out by the web page.

Using wildcards we can use string matching to find and display content based on what the user puts into that URI segment. In our "posts" Route let's add an array that we can match against ->

```
Route::get('/posts/{post}', function ($post) {
  // fake data store
  $posts = [
    'my-first-post' => 'Hello, this is my first blog post',
    'my-second-post' => 'Hello, this is my second post'
  ];

  //
    return view('post', [
      'post' => $post
    ]);
  });
