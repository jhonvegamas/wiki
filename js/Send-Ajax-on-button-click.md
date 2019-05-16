```HTML
<input id="name" type="text" name="user"/>
<input id="password" type="password" name="password"/>
<button id="btn-send" value="send" name="send">Send</button>
```
```JS
$(document).ready(function() {
  $("button").click(function(e) {
      e.preventDefault();
      $.ajax({
          type: "POST",
          url: "/pages/test/",
          data: { 
              name: $('#name').val(),
              password: $('#password').val(),
          },
          success: function(result) {
              alert('ok');
          },
          error: function(result) {
              alert('error');
          }
      });
  });
});
```
