# Laravel 01 - Intro, Routes, Blades #

> **Heads Up:** Laravel is what's called an MVC framework. MVC = Model-View-Controller. It divides an application into different aspects, or "separation of concerns". Each of the 3 main _concerns_ in an MVC framework handle functionally different parts of your application.

- The **Controller** receives requests and provides responses...it will delegate to fetch or write info from/to the database
- The **Model** is data, retrieving data, writing data. It receives requests from the Controller and uses what is called an eloquent model to run the SQL
- The **View** is the presentation of the data. It can be used to create a static html page, a template that is populated from a database, or even . It receives the data from the controller and renders it for the user

Request comes in and in the routes file load the necessary controller. Controller then delegates loading all the information necessary to the request then sends it to the view which presents it

## Routing ##
- Open Laravel project folder in your code editor
- The ```/Routes``` folder contains a file called ```web.php```. This file "routes" - or directs - requests that come from the "Web" (usually by typing a URL in the browser). In a nutshell, this file is where you register all routes for your application.
- The default route (as seen in the web.php file) handles requests that come in for the "root" of our site - aka ```/```.
- This request then triggers a closure (function) that returns a "view" function that returns the "welcome page" "blade" file to the requestor's browser.
- Blade files are in the resources/views folder
- Find the "welcome" blade file and change the heading ("Laravel") to something else (like, maybe your name?)
- Register a new "get" route for ```/welcome``` (hint: copy and paste the existing route and add ```welcome``` after the ```/```)
- In your browser try requesting ```192.168.10.10/```, then ```192.168.10.10/welcome```, then try anything else (like ```192.168.10.10/bob```) ...you will get 404 errors. This is because no routes have been set up for these URI segments.

> **Fun Fact:** The ```::``` is called the *Paamayim Nekudotayim* (which  means "double-colon" in Hebrew). It allows you to access the "original" versions of the methods and properties of a class that may have been changed or overwritten by a child class.

### Challenge ###
1. Register a new "get" route for ```/test```
2. Make sure that the new route returns the view of the ```'test'``` blade file. Should like like this ->
   ```
   Route::get('/test', function () {  
      return view('test');  
    });  
```
3. Create a new blade view file named ```test``` -> In the ```/resources/views/``` folder create a new file named ```test.blade.php```
4. Add basic boilerplate HTML -> !+TAB in a new CodePen project then copy and paste into this blade file OR manually type the HTML
5. Add an ```<h1>``` tag with the contents of ```Test```
6. Test by entering ```192.168.10.10/test``` in your browser

## Passing Request Data to Views ##
We can capture the variables set in the URL string of the request by "requesting" them from the Route (which reads them from the browser url). Add this route ->

```
  Route::get(‘/test-request’, function () {
    $name = request('name');

    return $name;
  });
```
Notice that we added ```test-request``` after the ```/``` and a var set using the ```request``` function (not related to the URI segment in the route). We also are not returning a view. Instead we are just going to display whatever the variable $name is set to.

After adding this route open your browser and type this as the URL request ```192.168.10.10/test-request?name=Bob```

Try it with different names! Make sure that ```name``` is always ```name```. The request function in your route is pulling the value for this from the URL, ```name=whateveryouwant```.

> **Heads Up:** The basic routing that we are learning here is just that, _basic_. The routing will get more complicated but we are learning the basics to help us fundamentally understand that requests sent to the Laravel framework from a browser (or API request, form request, etc) are not _pulling_ information. Requests to the framework are considered _input_ and we, as devs, program the framework to react to that input.

The next trick is to do something useful with that ```name``` data, like, maybe sending it to a blade file? Yes. Let's do that!

- We'll need to edit our route code to call a blade file ->  
```
  Route::get(‘/test-request’, function () {
    $name = request('name');

    return view('test-request');
    });
```
- Then we'll have to create a blade file named ```test-request.blade.php``` in the ```/resources/views/``` folder
  - Open the ```test-request``` blade file and add this code ->
```
  <p>{{ $name }}</p>
```
- Save everything, open your browser, and type the following into your browser's URL field -> ```192.168.10.10/test-request?name=Bob```
- You should see ```Bob``` displayed in your browser

> The "enclosure" characters **{{ }}** are a special directive that tells the Laravel framework to "echo" the contents within but first process whatever is in there through a series of encoding checks to remove bad stuff that could compromise your database, server, or Laravel

### Challenge ###
1. Create a new blade file called data.blade.php
2. In web.php create a new route to the blade file
3. The route should pass along at least 3 elements of data in an array to the blade file
4. Use @ directives in the blade file to iterate through and display each of the array elements passed to it…as a LIST!
