# Challenge: Serve A New HTML Site on Homestead #
## Objectives: ##
- Create a new folder in your ```Projects``` folder called ```mysite```
- Create an ```index.html``` file ("body" content is below)
- Create a ```main.css``` file (content below) — should be in a folder called ```css```
- "link" your css file in the html file
- In your ```Homestead.yaml``` file create new folder mapping and site mapping to your ```mysite``` folder - site will be called ```mysite.test```
- Add the ```mysite.test``` directive in your ```hosts``` file
- ```$ vagrant up``` To serve the site from your Homestead box
- Test by going to ```mysite.test``` in your browser

## Snippet of ```index.html``` ##
```
<div class="wrapper">
    <header class="main-head">The header</header>
    <nav class="main-nav">
        <ul>
            <li><a href="">Nav 1</a></li>
            <li><a href="">Nav 2</a></li>
            <li><a href="">Nav 3</a></li>
        </ul>
    </nav>
    <article class="content">
        <h1>Main article area</h1>
        <p>In this layout, we display the areas in source order for any screen less that 500 pixels wide. We go to a two column layout, and then to a three column layout by redefining the grid, and the placement of items on the grid.</p>
    </article>
    <aside class="side">Sidebar</aside>
    <div class="ad">Advertising</div>
    <footer class="main-footer">The footer</footer>
</div>
```

## Complete ```main.css``` file ##
```
nav ul li a {
  text-decoration: none;
}
nav ul li {
  list-style-type: none;
  margin: 5px;
}
body {
  padding:0px;
  margin:0px;
}
.main-head, .content, .main-nav, .side, .ad, .main-footer {
  background-color: gray;
  padding:20px;
}
.main-head {
  grid-area: header;
}
.content {
  grid-area: content;
}
.main-nav {
  grid-area: nav;
}
.side {
  grid-area: sidebar;
}
.ad {
  grid-area: ad;
}
.main-footer {
  grid-area: footer;
}

.wrapper {
  display: grid;
  grid-gap: 1px;
  grid-template-areas:
    "header"
    "nav"
    "content"
    "sidebar"
    "ad"
    "footer";
}

@media (min-width: 500px) {
  .wrapper {
    grid-template-columns: 1fr;
    grid-template-areas:
      "header"
      "nav"
      "content"
      "sidebar"
      "ad"
      "footer";
  }
  nav ul {
    display: flex;
    justify-content: space-between;
  }
}

@media (min-width: 700px) {
  .wrapper {
    grid-template-columns: 1fr 3fr;
    grid-template-areas:
      "header  header"
      "nav     nav"
      "sidebar content"
      "ad      footer";
  }
  nav ul {
    display: flex;
    justify-content: space-between;
  }
}

@media (min-width: 1000px) {
  .wrapper {
    grid-template-columns: 1fr 4fr 1fr;
    grid-template-areas:
      "header header  header"
      "nav    content sidebar"
      "nav    content ad"
      "footer footer  footer"
   }
   nav ul {
     flex-direction: column;
   }
}

```
