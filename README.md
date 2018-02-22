# Intro To jQuery

### Objectives
*After this lesson, students will be able to:*

- Describe what jQuery is and how to use it
- Include jQuery in your projects
- Practice using jQuery selectors


### Preparation
*Before this lesson, students should already be able to:*

- Use vanilla JavaScript to manipulate the DOM
- Use a text editor
- Be comfortable using CSS selectors

## jQuery - Intro (5 mins)

#### What is jQuery?
jQuery is a 3rd-party **library** that is intended to make front-end development tasks — particularly those involving DOM selection and manipulation — easier, faster, and more fun.

##### But wait, what do we mean by 'library'?
We've already seen that we can make our jobs easier and faster by using Node modules (AKA libraries) in our apps.

> A **library** is just a collection of reusable methods that serve a particular purpose. This is *different* from a **framework**, since we're ***still in control of the execution of our app*** (more on that in another lesson).




#### So, as a library, what does jQuery offer us?

jQuery helps us manipulate the DOM, allowing us to perform complex manipulations using less code with less hassle.  jQuery's syntax was developed to mimic CSS selector syntax, making code easier to develop, read, and manage; also, the syntax is more concise, and jQuery solves many cross-browser compatibility issues for us.

## Using jQuery - Demo (5 mins)

#### Installation
jQuery is a client side library, which means we need to include it in our HTML. To do this, we have two options:

1. Reference jQuery from a server on the internet:

  - Directly from jQuery's website (http://code.jquery.com/)
`https://code.jquery.com/jquery-3.2.1.slim.min.js`
  - From a CDN (content delivery network) like [CDNJS](https://cdnjs.com/) or [Google Hosted Libraries](https://developers.google.com/speed/libraries/)
2. Download jQuery and put it in your `src` folder!


#### What's with the 'slim.min.js' in the name of the jQuery file?

If you look carefully at the filenames of the jQuery versions you download, or just look at the URL in the "src" attribute for each script tag above, you'll notice something at the end of each file name — namely, that they end in 'min.js'. This means the JavaScript code has been minified.

Minification is the process of making a JavaScript file smaller by, among other things, removing all line breaks and whitespace, reducing the length of variable and function names, and stripping out all comments. Minification can significantly reduce the size of a JavaScript file, and in turn, significantly decrease the time it takes our browsers to load the file into memory.

In jQuery's case, the original unminified code is about 286 kilobytes, whereas the minified code is only 87 kilobytes. That makes the minified version **one-third** the size of the original - not bad!

Minified scripts can be difficult to read, so most servers that host jQuery and other libraries will also offer the original (non-minified) version of the code so developers can understand the code.

Minification is performed on a JavaScript when it's ready for release and there are many options for doing this. If you'd like to minify your own scripts, try a Google search to check out the various options. Also, if you do happen to come across a library where you can't find a non-minified version to look at, software also exists to decompress a minified script. These are usually called unminifiers, pretty-printers, or beautifier). They take a minified JavaScript and attempt to decompress it, making it easier to read and understand.

**Even if you don't fully understand the code, it's a good exercise to visit code.jquery.com and take a look at minified and non-minified jQuery.**

## Slim??
In addition to minification, jQuery has released a "slim" version of its library that removes most of the legacy code, in addition to the things that have become more standard in the JS language. This brings the total file size down to 70K.


## DOM manipulation with jQuery

Before we get into jQuery, let's just think about how we would perform the following tasks:

  - `select` a DIV and change its content
  - `append` a new DIV with some content to a web page
  - `listen` for events on a collection of DIVs or other HTML elements
    - For example, a blog site might have a "like" button for each comment on a post.

#### First, let's just talk about selecting an element with jQuery

To select an element in the DOM, we use the global jQuery function. Note that this is almost identical to the newer document.querySelector method we've been using. 

```JavaScript
// This is the basic syntax for jQuery selections
$(' ')

// To select a particular element by tag, you do
$('h2') // selects all h2 elements

// To select by ID, you use the same syntax as CSS selectors
$('#some-id') // Would select the element with ID="someID"

// To select all elements of a particular class, use CSS syntax again
$('.some-class') // Selects all elements of the class "someClass"

// And you can use more complicated CSS3 selectors as well
$('p.another-class') // Selects all <p> tags that also have the class "anotherClass" (<p class="anotherClass")
```

If you use variable assignment when doing a selection, a "jQuery" object is returned

```JavaScript

// We prepend '$' to variable names when a variable is going to be a jQuery object to help us remember what that variable is for.
var $jqObject = $('p'); // Returns a jQuery object containing all <p> tags on your web page.

// However, we don't have to prepend '$' to our variables. It's just so we can remember what a variable is being used for.
var jqObject = $('p'); // This is functionally identical to the version above that includes the '$' in front of jqObject.
```

#### Selecting a DOM element and changing it's content

In this HTML:


```html
<div id="my-div">Hello world!</div>
```

```JavaScript
const divToManipulate = document.getElementById('my-div');
divToManipulate.innerHTML = 'Goodbye world!';
```

Now the code above isn't too hard to deal with, but even so, in jQuery, this is a one-liner.

```javascript
$('#my-div').html('Goodbye world!');
```

If we wanted to **save our selection as a jQuery object**, the code would look like this instead:

- First we select the element we want and save it as a jQuery object

```javascript
const $myDiv = $('#my-div');
```

- Then we use our jQuery object to perform our task

```javascript
$myDiv.html('Goodbye world!');
```

There are three things about the example above that make jQuery easier to use:

  1. jQuery is using the same syntax as CSS to select elements
  2. jQuery allows us to chain methods together to accomplish our goals (e.g., ```$().html(...)``` ), making code shorter and easier to understand
  3. jQuery deals with any cross-browser compatibility issues, which may not seem like a big deal in this example, but which quickly become difficult to deal with as things get more complex

#### Appending a DOM element to a web page

If we had the following HTML page...

```html
<html>
<body>
  <div id="container"></div>
</body>
</html>
```

If we want to add a new DIV that provides a nice greeting, our vanilla JavaScript would have to be:

```javascript
  const myDiv = document.getElementById('container');
  const newP = document.createElement('p');
  newP.innerHTML = 'Hello complicated, multi-step world of adding an element to the DOM!';
  myDiv.appendChild(newP);
```

And in jQuery, it looks like this:

```javascript
  $('#container').append('<p>').append('Hello simple insertion using jQuery chaining');
```

In the jQuery code example above, we first select the DIV with `id="container"`, then we append a new paragraph element (automatically created using core jQuery selector function), and then we append the text we want to insert to the new paragraph element we just created. In effect, the new HTML looks like this after the jQuery is run:

```html
  <div id="container">
    <p>
      Hello simple insertion using jQuery chaining
    </p>
  </div>
```


#### Modifying Styles (CSS) Using jQuery

You can do more than select elements and modify content. You can also create or update CSS style attributes in jQuery using the .css() method

```js
$('#my-div').css('color', 'red');
```

The code above will change the color of all text inside the DIV with id="myDiv" to red.

Or, if we have a bunch of elements that all have the same class (in this example, it's class="myClass"), we can use the class selector to modify the color of all of them at once:

```js
$('.my-class').css('color', 'blue');
```

But that seems kind of boring. I mean, what if we want to do something with less hard-coding using jQuery.

```javascript
var randColorValue = function() {
  return Math.floor( Math.random() * 255 );
};

var randColor = function() {
  var red = randColorValue();
  var green = randColorValue();
  var blue = randColorValue();

  return `rgb(${red}, ${green}, ${blue})`;

}

$('.my-class').css('color', randColor() );
```

#### Adding and Removing Elements Using jQuery

Sometimes in a dynamic web application, user-input is meant to trigger the addition or removal of content or functionality. Using jQuery, we can easily create new DOM elements and insert them into the DOM, or remove existing elements (and any content they contain) from the DOM.

So, let's imagine we have a web page with the following content on it:

```html
<body>
  <div id="outer-container">
    <div class="inner-item inner-item-header">Enjoy some hipster ipsum:</div>
    <div class="inner-item">
      Aesthetic migas paleo McSweeney's, pork belly Kickstarter Echo Park sriracha keytar disrupt viral drinking vinegar fanny pack typewriter.
    </div>
  </div>
</body>
```

Let's say we want to add some more hipster ipsum to the page. Something like:

```html
<div class="inner-item">
	Farm-to-table Godard roof party bespoke, fashion axe mustache vinyl.
</div>
```

To add this DIV, and our hipster ipsum content using jQuery, we'd do the following:

Define a new DIV and assign jQuery object to $newDiv

```javascript
const $newDiv = $('<div>');

// Add hipster ipsum content
$newDiv.html("Farm-to-table Godard roof party bespoke, fashion axe mustache vinyl.");

// Set it's class to innerItem
$newDiv.addClass("inner-item");

// Append our new element  
$('#outer-container').append($newDiv);
```


See this in action (and play around with it) [on JSBin](http://jsbin.com/gupade/3/edit?html,js,output)


## 🚀 LAB: Reddit

Following the directions below to practice using jQuery:

- Go to http://www.reddit.com

- Reddit uses jQuery, so we can use our Chrome developer console to manipulate the site in real time using jQuery.

- To do this, once Reddit.com has loaded, go to your view menu in Chrome. Select View > Developer > JavaScript Console

- Once that's loaded, try entering the following command into the Chrome REPL:

```javascript
$('img').hide()
```

- Hit enter. All the images should have disappeared from the Reddit.com home page. Make sure you understand why before moving on.

- Now try this:
```js
$('img').show()
```

- That should have brought all the images back. Make sense so far?

- Now with the chrome inspector, try to match the title of the first Reddit post and replace the text using `.text()` or `.html()`.

- Try to replace the blue background in the header by another color using the function `.css()`.

- Now try some of the other examples we've gone over in the Chrome REPL and see what happens to the Reddit.com website. Remember, this is your laboratory — your chance to experiment and learn. Make use of it.

## 🚀 LAB: Duck Hunt

Make a fork of [this codepen](https://codepen.io/jlr7245/pen/oEdmyr?editors=0010) and follow the instructions!!

## Conclusion

- jQuery makes JavaScript super friendly and easy to write. a lot of websites are using jQuery, soon you will too.  Remember that it's always good to know how to use what is called vanilla JavaScript, or JavaScript without a library.

- Please spend some time reviewing [the documentation](https://api.jquery.com/).
