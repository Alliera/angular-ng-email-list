ng-email-list
=============

A angularjs directive that parsers a textarea into an array of valid email addresses.

#Installation

```
  npm install ng-email-list
```

You can either self host the script found in `dist/ng-email-list.js` or use browserify.

```
<!--self host-->
  <ng-email-list ng-model="emails"></ng-email-list>
  <script scr="/angular.js"></script>
  <script src="/ng-email-list.js"></script>
  ...
  <script>
    //main file
    angular.module('myApp', ['ng-email-list']);
  </script>
```

```
  //browserify
  require('ng-email-list');
  angular.module('myApp', ['ng-email-list']);
```

#Usage

    <ng-email-list ng-model="emails"></ng-email-list>

Optional Usage:

    <ng-email-list ng-model="model" rejected="rejects" repeat="repeats"></ng-email-list>

If you are using angular 1.3 or greater you can debounce the input:

    <ng-email-list ng-model="emails" ng-model-options="{debounce : 1000}"></ng-email-list>

NOTE: If you want your model value to be updated even on invalid input, set the
`ng-model-options="{allowInvaid: true}"`

    <ng-email-list ng-model="emails" ng-model-options="{allowInvalid : true}"></ng-email-list>

##Model

Model will be set with an array of valid email address. If the repeat option is specified, it will not contain repeats. 

##Rejected (Optional)

An array of invalid email addresses. Perfect for displaying more useful error messages.

##Repeat (Optional)

An array of repeated email addresses. Perfect for displaying more useful error messages. **WARNING:** This feature is incompatible with IE8 or below.

##Form Validity

If you use the email-list with angulars form validity you get access to the following options: `email`, `repeat`, and `invalid`.

The `email` error is set if there are one or more invalid emails.

The `repeat` error is set if there are one or repeated emails. This error will only be set if you set the repeat property. **WARNING:** This feature is incompatible with IE8 or below.

The `invalid` error is set if there are invalid or repeated emails. Repeated emails are only check if the repeated property is set.

###Form Validity Example

You can display human friendly error messages in the following manner:

```
<form name="myForm">
  <email-list name="list" ng-model="emails" rejected="rejects" repeat="repeats"></email-list>
  <div ng-show="inviteForm.list.$error.emailList">
      <p>The email list is invalid!</p>
  </div>
  <div ng-show="inviteForm.list.$error.email">
      <p ng-show="rejects.length === 1">The following email is invalid {{rejects[0]}}</p>
    <p ng-show="rejects.length > 1">The following emails are invalid: {{rejects.join(', ')}}</p>
  </div>
  <div ng-show="inviteForm.list.$error.repeat">
      <p ng-show="repeats.length === 1">The following email is repeated:{{repeats[0]}}</p>
      <p ng-show="repeats.length > 1">The following emails are repeated:{{repeats.join(', ')}}</p>
  </div>
</form>
```

#Developers Guide

Clone this repository and then run `npm install`.

Building the project use `make`. This will create the dist files. You will need
browserify and uglifyjs installed globally. You can test your dist bundles using
the test.html file.

Testing the project use `make test`. This will run the karma tests.
