# CDN's

```HTML
<script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-validate/1.19.0/jquery.validate.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/sweetalert2@8"></script>
```

# Code

```HTML
<form id="registroForm" action="#">    
    <input type="text" name="name" placeholder="Names *" class="form-control required">                
    <input type="text" name="phone" placeholder="Phone *" class="form-control required">    
    <input type="email" name="email" placeholder="Email *" class="form-control required">
    <textarea name="message" placeholder="Message *" cols="30" rows="10" class="form-control required"></textarea>
    <button type="submit" class="btn">SEND</button>                        
</form>
```


```JS
$('#registroForm').validate({
    ignore: ":hidden",
    rules: {
        name: {
            required: true,
            minlength: 3
        },
        phone: {
            required: true,
            number: true
        },
        email: {
            required: true,
            email: true
        },
        message: {
            required: true,
            minlength:7,
            maxlength:10
        }
    },

    messages: {
        name: {
            required: 'The name is required.',
            minlength: "This field requires at least 3 characters"
        },
        phone: {
            required: 'The phone is required.',
            number: 'Phone not valid.'
        },
        email: {
            required: 'Email is required',
            email: 'Email not valid.'
        },
        message: {
            required: 'The message is required.',
            minlength:"This field requires a minimum of 7 characters",
            maxlength:"This field requires a maximum of 10 characters"
        }
    }, submitHandler: function(form) {

      Swal.fire({
       title: 'Sending data', html: 'Wait a moment please',	onBeforeOpen: () => {
         Swal.showLoading()
           timerInterval = setInterval(() => {})
         },
         onClose: () => {
           clearInterval(timerInterval)
         }
     });

      $.post("service url",$(form).serialize(),function(result){
        if(result.response == "error") {
            Swal.close();                        
            Swal.fire(
              'Service failed',
              '',
              'warning'
            )
        } else {
            Swal.close();
            Swal.fire(
              'Success',
              '',
              'success'
            )                        
            form.reset();
        }
      }).fail(function() {
          Swal.fire(
            'Ups!',
            'Something is not working well, try later or contact support if the problem persists',
            'warning'
          )
      });
        return false;
    }
});
```
