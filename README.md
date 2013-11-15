# knockoutjs-file-binding

For use with [Knockout.js](https://github.com/knockout/knockout): a binding that stores an encoded file
(from an input element) in an observable.

## Usage

You can pass a single observable to the binding, and it will assign it the base64 encoded representation of the file.

```html
<input type="file" data-bind="file: fileInput">

<script>
  var viewModel = {
    fileInput: ko.observable()
  }
  
  ko.applyBindings(viewModel);
</script>
```

You can also pass an object to the binding like so:

```html
<input type="file" data-bind="file: {data: fileInput, name: fileName}">

<h1 data-bind="text: fileName"></h1>

<output data-bind="text: fileInput"></output>
```

<code>data</code> is the only key that is required. The optional key <code>name</code> will assign the filename
to its observable. The <code>prohibited</code> key accepts either a string or array of strings. Those content types
(<code>text/javascript</code>, etc) will be ignored. <code>allowed</code> is similar, but ignores everything except
the listed content types.

The file binding internally creates a new <code>FileReader</code> object to do the encoding. To use an existing one and prevent
a new one from being created, pass it through the <code>reader</code> key.

```html
<input type="file" data-bind="file: {data: fileInput, reader: someReader}">

<script>
  var viewModel = {
    fileInput: ko.observable(),
    someReader: new FileReader()
  }
  
  ko.applyBindings(viewModel);
</script>
```
