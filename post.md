# post title - something about frameworks

## The Document Object Model

A web browser displaying a web page has, in it's memory, a 'Document Object Model' (the DOM). This is the structure containing all of the information to display the page - the title, the headings, the links, the paragraphs, the buttons - everything.

```
Document
│
└── <html lang="en">
    │
    ├── <head>
    │   │
    │   ├── <meta charset="UTF-8">
    │   │
    │   ├── <title>
    │   │   └── "My Website"
    │   │
    │   └── <link rel="stylesheet" href="style.css">
    │
    └── <body>
        │
        ├── <button id="counter">
        │   └── "You clicked 0 times"
        │
        └── <script>
            └── [JavaScript code]
```

The browser uses this to display the page, but also, we can manipulate it with Javascript. For example, if we want to change the title of the page above, it could look like this:

```js
  document.title = "My New Page Title";
```

`title` is sort of a special case, usually if we want to select an element we'd probably search the DOM for it with something like:
```js
  document.querySelector("title").textContent = "My New Page Title";
```
This style works for any element, for example:
```js
  document.querySelector("button").textContent = "Press me";
```

Perhaps button is a bit general, for example it's not clear which button will have it's text changed if we have several buttons. The button above (helpfully) has an `id`, so we can use that:
```js
  document.getElementById('counter').textContent = "Press me";
```

The element returned by a query selector is an object, so usually we'd save it to a variable to avoid repeating the select and to make the code readable.
```js
  const button = document.getElementById('counter');
  button.textContent = "Press me";
```

There's many methods on `document` in addition to `querySelector()` and `getElementById()`. One of the common things we want to do is to capture events so we can execute code based on the user interaction with our elements. Usually for a button, we'd like to do something when the user clicks it:
```js
    const button = document.getElementById('counter');

    button.addEventListener('click', () => {
      console.log('clicked');
    });
``` 

## Our dynamic page

That's enough background for you to understand this:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Clicked x times</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <button id="counter">You clicked 0 times</button>

  <script>
    let count = 0;

    const button = document.getElementById('counter');

    button.addEventListener('click', () => {
      count++;
      button.textContent = `You clicked ${count} times`;
    });
  </script>
</body>
</html>
```

We have a simple web page containing a single button. We're selecting that with `getElementById('counter')` which works because we have it that ID in the HTML `<button id="counter">`. When the user clicks on the button, our click code runs incrementing the counter and updating the text on the button.

If you open this page in a web browser, you can click on the button