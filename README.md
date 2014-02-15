Flashback
=========
A tool to convert JSON objects into beautiful form errors.

To Do
======
Before you dive in, please read through all of the issues as these define what this thing really is. They are the specifications. There are surely things out there that already exist, so we should be aware of what they are. If there is something that already does the job well, then we should use it instead of creating this project. If there is something similar but not similar enough, we should use it as inspiration. Please list all similar tools at the bottom of this readme.

Inspiration
===========
- [Walk [Your City] Login/Registration Form](http://walkyourcity.org/login)
- [GitHub: cjroth/formstrap](https://github.com/cjroth/formstrap)
- [jQuery Basic Plugin Creation](http://learn.jquery.com/plugins/basic-plugin-creation/)

Alternatives
============
- Fill me in with an alternative project!
- And me!
- Me too!

How It Works
============
let's say you have a form called "registration":
```
<form id="registration">
  <!-- ... all of the form content would be here... -->
</form>
```

then you use jquery to override the form's submit behavior:
```
$('#registration').submit(function() {
  var $form = $(this);
  $.post('http://api.farmathand.com/v1/register', $form.serialize())
    .error(onError) // onError is defined below
    .success(function(data) {
      // do something with the data
    })
  return false;
})
```

and when there is an error, we pass it to the flashback method:
```
onError = function(err) {
  // pass the error to flashback
  $form.flashback(err);
}
```

Errors
======
errors will be in the format:
```
{
  "form": [
    "This is an error that applies to the entire form."
  ],
  "email": [
    "Email is invalid.",
    "Email is too long. The maximum length is 250 characters."
  ],
  "password": [
    "Password cannot be empty."
  ],
  "first_name": [
    "First name is empty."
  ],
  "last_name": [
    "Last name is too long. The maximum length is 30 characters."
  ]
}
```
