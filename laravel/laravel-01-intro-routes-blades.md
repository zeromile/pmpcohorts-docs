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
2. Create a new blade view file named ```test```
3. Add the basic boilerplate HTML (!+TAB in a new CodePen project then copy and paste into this blade file)
4. Test by entering ```192.168.10.10/test``` in your browser

## Passing Request Data to Views ##
We can capture the variables set in the URL string of the request by "requesting" them from the Route
