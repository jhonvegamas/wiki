# CDN's
```HTML
  <script src="https://cdn.jsdelivr.net/npm/sweetalert2@8"></script>
  ```
  
# Register

## HTML
```HTML
<button style="background-color: #3897f0; border: 1px solid #3897f0; border-radius: 4px; color: #fff; position: relative; padding: 10px; width: 100%" id="facebook-login" onclick="login()">
    <span class="coreSpriteFacebookIconInverted cneKx"></span><strong>Log in with Facebook</strong>
</button>
```

## Java Script
```JS
<script>
  var facebookAppID	= '{api-key-facebook}';
  var fbUser = {};
  var facebook_connect = function (){
      //this method is executed when connected
  };
  var facebook_register	= function () {
      //Get data user
      FB.api('/me',{fields: 'name, first_name, last_name, email'}, function(response) {
          fbUser = response;
          console.log('first_name' + fbUser.first_name);
          console.log('last_name' + fbUser.last_name);
          console.log('email' + fbUser.email);
          console.log('id' + fbUser.id);       
      })
  };
  //	Function to call when the person is connected to Facebook, but not to your application
  var facebook_notAuthorized	= function () {
      console.log('It is necessary to connect to the application.');
  };
  //	Function to call if the person is not connected to Facebook
  var facebook_notConnected	= function () {
      console.log('It is necessary to be connected to Facebook.');
  };
  //	Initiated asynchronously by FB.getLoginStatus()
  var statusChangeCallback	= function (response) {
     console.log('____________________');
     console.log('statusChangeCallback');
     console.log(response);
     console.log('____________________');

    if (response.status === 'unknown') {
    }
    //	Correct login and authorization
    if (response.status === 'connected') {
        facebook_connect();
    //	Login correct, without authorization
    } else if (response.status === 'not_authorized') {
        facebook_notAuthorized();
    } else {
    //	User not connected to Facebook
        facebook_notConnected();
    }
  };
  // *******************************************************
  //		Start the Facebook SDK asynchronously
  // *******************************************************
  window.fbAsyncInit	= function() {          	
      FB.init({
          appId      : facebookAppID,
          cookie     : true,
          xfbml      : true,
          version    : '{version-api-facebook}'
      });

      FB.getLoginStatus(function(response) {
          statusChangeCallback(response);                
      })
  };
  // *******************************************************
  //		Upload the Facebook SDK asynchronously
  // *******************************************************
  (function(d, s, id) {
    var js, fjs = d.getElementsByTagName(s)[0];
    if (d.getElementById(id)) return;
    js = d.createElement(s); js.id = id;
    js.src = "//connect.facebook.net/en_US/sdk.js";
    fjs.parentNode.insertBefore(js, fjs)
  }(document, 'script', 'facebook-jssdk'))

  function login() {
      FB.login(function(response) {
        if (response.status === 'connected') {
            facebook_register();
        }
      }, {scope: 'email, public_profile'});
    }
</script>
```

# Login

```JS
<script>
  var facebookAppID	= '{api-key-facebook}';
  var fbUser = {};
  var facebook_login	= function () {
    FB.api('/me',{fields: 'name, first_name, last_name, email'}, function(response) {
    fbUser = response;
      Swal.fire({
          title: 'Validating information',
          html: 'wait a moment please',
          onBeforeOpen: () => {
            Swal.showLoading()
            timerInterval = setInterval(() => {})
          },
          onClose: () => {
            clearInterval(timerInterval)
          }
      });
      $.get("{url-service-login}", {id: fbUser.id, email: fbUser.email, first_name:fbUser.first_name, last_name:fbUser.last_name})
      .done(function( data ) {
        Swal.close();
        if (data === 'true') {
            window.location.reload();
        } else{
            Swal.fire(
                'User not found',
                'You are not registered with facebook',
                'warning'
            )
        }
      }).fail(function(data) {
          Swal.close();
          Swal.fire(
              'Ups!',
              'Something does not work well, if the problem persists, contact support.',
              'warning'
          )
          console.log(data);
      });
    })
  };
  var statusChangeCallback	= function (response) {
      if (response.status === 'connected') {
          FB.logout();
          window.location.reload();
      }
  };  
  window.fbAsyncInit	= function() {    
    FB.init({
      appId      : facebookAppID,
      cookie     : true,
      xfbml      : true,
      version    : 'v3.2'
    });
    FB.getLoginStatus(function(response) {
        statusChangeCallback(response);
    })
  };
  (function(d, s, id) {
    var js, fjs = d.getElementsByTagName(s)[0];
    if (d.getElementById(id)) return;
    js = d.createElement(s); js.id = id;
    js.src = "//connect.facebook.net/en_US/sdk.js";
    fjs.parentNode.insertBefore(js, fjs)
  }(document, 'script', 'facebook-jssdk'))

  function login() {
      FB.login(function(response) {
        if (response.status === 'connected') {
            facebook_login();
        }
      }, {scope: 'email'});
    }
</script>
```

# Logout

add this function in js
```JS
function logout() {
  FB.logout(function (response) {
      window.location.reload();
  });
}
```
