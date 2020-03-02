# Laravel 01 - Intro, Routes, Blades #

> **Heads Up:** Laravel is what's called an MVC framework. MVC = Model-View-Controller. It divides an application into different aspects, or "separation of concerns". Each of the 3 main _concerns_ in an MVC framework handle functionally different parts of your application.

- The **Controller** receives requests and provides responses...it will delegate to fetch or write info from/to the database
- The **Model** is data, retrieving data, writing data. It receives requests from the Controller and uses what is called an eloquent model to run the SQL
- The **View** is the presentation of the data. It can be used to create a static html page, a template that is populated from a database, or even . It receives the data from the controller and renders it for the user

Request comes in and in the routes file load the necessary controller. Controller then delegates loading all the information necessary to the request then sends it to the view which presents it

## Routing ##
- Open the Laravel project folder in your code editor
- The ```/Routes``` folder contains a file called ```web.php```. This file "routes" - or directs - requests that come from the "Web" (usually by typing a URL in the browser). In a nutshell, this file is where you register all routes for your application.
- The default route (as seen in the web.php file) handles requests that come in for the "root" of our site - aka ```/```.
- This request then triggers a closure (function) that returns a "view" function that returns the "welcome page" "blade" file to the requestor's browser.
- Blade files are in the resources/views folder
- Find and open the "welcome" blade file (```welcome.blade.php```) and change the h1 heading from ```"Laravel"``` to something else (like, maybe your name?). Save your file!
- In the ```web.php``` file register a new "get" Route for ```/welcome``` (hint: copy and paste the existing Route and add ```welcome``` after the ```/```)
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
Notice that we added ```test-request``` after the ```/``` and a var set using the ```request``` helper function (not related to the URI segment in the route). This request helper is looking for a key in the URL string called ```name``` and setting the variable named ```$name``` to be whatever that request helper finds for the ```name``` key. We are not returning a view. Instead we are just going to display whatever the variable ```$name``` is set to.

After adding this route open your browser and type this as the URL request ```192.168.10.10/test-request?name=Bob```

Try it with different values for name! The request helper function in your route is pulling the value for this key from the URL, ```name=whateveryouwant```.

> **Heads Up:** The basic routing that we are learning here is just that, _basic_. The routing will get more complicated but we are learning the basics to help us fundamentally understand that requests sent to the Laravel framework from a browser (or API request, form request, etc) are not _pulling_ information. Requests to the framework are considered _input_ and we, as devs, program the framework to react to that input.

The next trick is to do something useful with that ```$name``` data, like, maybe sending it to a blade file? Yes. Let's do that!

- We'll need to edit our route code to call a blade file ->  
```
  Route::get(‘/test-request’, function () {
    $name = request('name');

    return view('test-request');
    });
```
- Unfortunately, this code will not automatically pass the $name variable to the ```test-request``` blade file. Remember, variables set inside of functions are scoped to that function only...unless we pass them along in a functions call (or set them as part of a global object). Because ```view()``` is a function we're calling, we can include data as an additional parameter.  
- The first parameter of the view function is the name of the blade file. The second, optional, parameter can be an array that contains key=>value pairs. In our case we will set a key's value to the value of the ```$name``` variable. Our new code will look like this ->
```
  Route::get(‘/test-request’, function () {
    $name = request('name');

    return view('test-request', [ 'name' => $name ]);
    });
```
- Then we'll have to create a blade file named ```test-request.blade.php``` in the ```/resources/views/``` folder
  - Open the ```test-request``` blade file and add this code ->
```
  <p>{{ $name }}</p>
```
> **Heads Up:** The "enclosure" characters **{{ }}** are a special directive that tells the Laravel framework to "echo" the contents within but first process whatever is in there through a series of encoding checks to remove bad stuff that could compromise your database, server, or Laravel
- Save everything, open your browser, and type the following into your browser's URL field -> ```192.168.10.10/test-request?name=Bob```
- You should see ```Bob``` displayed in your browser


### Challenge ###
1. Add more request helpers to the Route that will find keys ```age``` and ```city```.
2. pass those variables in the view function as additional key=>value pairs in the view function array parameter.
3. Echo those variables in the ```test-request``` view file using the {{}} enclosure characters
