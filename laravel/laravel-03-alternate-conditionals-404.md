# Laravel 03 - 404,  #

### Review ###
- ```[]``` defines an array
- ```{{}}``` defines an enclosure in a blade file
- ```,``` separates items such as parameters in a function call or key=>value pairs in an array
- ```;``` ends a complete statement in PHP
- ```{}``` defines a wildcard in a Route declaration

> **Heads Up:** Because our routes files are handling every request, we need to be able to


```
Route::get('/posts/{post}', function ($post) {

    return view('post', [
      'post' => $post
    ]);
  )}
```


## Title ##

### Challenge ###
