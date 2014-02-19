Flashback
=========
A tool to convert JSON objects into beautiful form errors.

# Usage

With Defaults:
```
$('#my-form').flashback();
```

With Configuration:
```
$('#my-form').flashback({

  // redirect to url when form submits successfully
  redirect: 'http://mywebsite.com/redirect-to-me-when-successful',

  // post form data to url (equivalent to the "method" attriute on the <form> tag)
  url: 'http://mywebsite.com/post-form-data-here',

  // method, as in post, get, put, delete, etc
  method: 'post',

  // custom function for parsing your errors
  parser: function(errorObject) {
    // ...
    return errorObject;
  },

  // custom function for decorating your errors with html
  decorator: function(errorsArray, fieldName) {
    // ...
    return myHTML;
  },

  // custom function for injecting your errors into the dom
  renderer: function(fields) {
    var $form = this;
    // ...
  },

  // do this when the form submits successfully
  success: function(data) {
    // ...
  }
});
```
jQuery Flashback works with *any* error object format, so no matter how your
server formats errors to the client, it will work as long as they are valid
JSON and have a failing status code (>= 400). To use it, just write a function
to coerce your errors into this global format, mapping field names to arrays
of string error messages:

```
{
  "email": ["There is already a user registered with that email."],
  "password": ["There is already a user registered with that email."]
}
```

It is totally unopinionated about how errors should be rendered or what frontend
frameworks you might want to use, so you can use it with Bootstrap, UIKit, or
no framework at all. By default, errors are divs with the class "form-error":

```
<div class="form-error">This is an error message.</div>
```

But you can change this by supplying a decorator function. And you can change the
location within the form that it injects these errors by supplying a renderer
function.

You can use it right out of the box using just some basic CSS:

```
.form-error {
  color: #f00;
  font-weight: bold;
}
```

Flashback will check the form element itself for configuration attributes too:

```
<form id="myform" data-redirect="/woot">
```

Is equivalent to:

```
$('#my-form').flashback({ redirect: '/woot' });
```