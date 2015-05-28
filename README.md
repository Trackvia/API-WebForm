# API-WebForm

## Features

This project is an example web form using the TrackVia API.  The form must be
hosted on a web server with access to the included Javascript files.

## Requires

1.  TrackVia Account 

http://www.trackvia.com

2.  TrackVia Javascript SDK

https://github.com/Trackvia/API-Javascript-SDK
 

## Usage

1.  Enable API access in your TrackVia Account
2.  Create a user a limited user in the account
3.  Grant the user access to create records only via a Role
4.  Get the view id that will be used for creating records
5.  Modify the form and code to match the field names that will be created in
    the view


## Sample HTML

```HTML

 <body>
    <div class="container">
        <div class="row clearfix">
            <div class="col-md-12 column">
                <div class="container-fluid">
                    <h3 class="text-center"><small>Enter your information</small></h3>
                    <form id="signupForm" role="form" data-toggle="validator" data-disable="false" novalidate>
                      <div class="form-group">
                        <label for="inputFirstName">First Name *</label>
                        <input type="text" name="name" class="form-control" id="inputFirstName" placeholder="Enter first name" required>
                        <div class="help-block with-errors"></div>
                      </div>
                      <div class="form-group">
                        <label for="inputLastName">Last Name *</label>
                        <input type="text" name="name" class="form-control" id="inputLastName" placeholder="Enter last name" required>
                        <div class="help-block with-errors"></div>
                      </div>
                      <div class="form-group">
                        <label for="inputCompany">Company *</label>
                        <input type="text" name="company" class="form-control" id="inputCompany" placeholder="Enter company name" required>
                        <div class="help-block with-errors"></div>
                      </div>
                      <div class="form-group">
                        <label for="inputEmail">Email *</label>
                        <input type="email" name="email" class="form-control" id="inputEmail" placeholder="Enter email" required>
                        <div class="help-block with-errors"></div>
                      </div>
                      <div class="form-group">
                        <label for="inputPhone">Phone Number *</label>
                        <input type="tel" name="phoneNumber" class="form-control" id="inputPhone" placeholder="Enter phone number" pattern="^\s*(?:\+?(\d{1,3}))?[-. (]*(\d{3})[-.)]*(\d{3})[-. ]*(\d{4})(?: *x(\d+))?\s*$" required>
                        <div class="help-block with-errors"></div>
                      </div>
                      <div class="form-group">
                        <button type="submit" class="btn btn-primary">Submit</button>
                      </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
  </body>


```

## Sample Javascript

```javascript
var tv = new TrackVia(
    'YOUR_API_KEY',
    'YOUR_USER_EMAIL',
    'YOUR_PASSWORD',
    'TrackViaAPI');
```

Get a list of views and record
```javascript
        $(document).ready( function() {
            $("#signupForm").submit(function() {
                var tv = new TrackVia(
                    '<YOUR_API_KEY>',
                    '<YOUR_USERNAME>',
                    '<YOUR_PASSWORD>',
                    'TrackViaAPI');
                
                tv.login().done (function() {
                   
                    var contact = getFormData();
                    var record = null;
                    tv.createRecord( <YOUR_VIEW_ID> , contact).done(function(response) {
                        record = response.data;
                        if ( record != null ) {
                            alert("Success");
                        }
                    });
                    
                 });
                
                return false; // avoid to execute the actual submit of the form.
        
        });
        function getFormData() {
            var data = {
                "First Name" : $("#inputFirstName").val(),
                "Last Name" : $("#inputLastName").val(),
                "Company Name" : $("#inputCompany").val(),
                "Email Address" : $("#inputEmail").val(),
                "Phone Number" : $("#inputPhone").val()
            };
            return data;
        }
    } );
```

