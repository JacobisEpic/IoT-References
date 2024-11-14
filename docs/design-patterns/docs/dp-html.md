# Design Pattern – html

Hypertext Markup Language (HTML) is a markup language for creating
webpages. Markdown is another markup language, albeit a super
lightweight but friendly one. HTML files are usually stored at a web
server. A web browser then fetches, renders, and displays the HTML
files as a webpage.

JavaScript can make a web page more dynamic. Here's a basic pattern to follow:

```html
<!-- This is a comment-->
<!DOCTYPE html>
<html>

  <!-- This is the HTML Head -->
  <head>

    <!-- Page title -->
    <title>Test Website</title>
    <!-- You can embed CSS files either in the head or linked to them -->
    <link rel="stylesheet" href="../css/style.css">
    <style type="text/css"></style>

  </head>

  <!-- Body -->
  <body>

    <!-- paragraph -->
    <p>Hello World!</p>
    <!-- Division -->
    <div id="test"> </div>

    <!-- Scripts  -->
    <script src="/socket.io/socket.io.js"></script>
    <script>Some script</script>

  </body>
</html>
```
JavaScript can change HTML content, styles, and attributes:
```js
// JavaScript to change HTML content
document.getElementById("demo").innerHTML = "Hello JavaScript!";

// JavaScript to change HTML styles
document.getElementById("demo").style.fontSize = "25px";
document.getElementById("demo").style.color = "red";
document.getElementById("demo").style.backgroundColor = "yellow";

// JavaScript to change HTML attributes
document.getElementById("image").src = "picture.gif";
```


## References
- [HTML Tutorial](https://www.w3schools.com/html/default.asp)
