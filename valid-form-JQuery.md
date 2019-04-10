# CDN's

```HTML
<script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-validate/1.19.0/jquery.validate.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/sweetalert2@8"></script>
```

# Code

```HTML
<form id="registroForm" action="#">    
    <input type="text" name="name" id="name" placeholder="Names *" class="form-control required">                
    <input type="text" name="phone" id="phone" placeholder="Phone *" class="form-control required">    
    <input type="email" name="email" id="email" placeholder="Email *" class="form-control required">
    <textarea name="message" id="message" placeholder="Message *" cols="30" rows="10" class="form-control required"></textarea>
    <button type="submit" class="btn">SEND</button>                        
</form>
```


```JS
$('#registroForm').validate({
    ignore: ":hidden",
    rules: {
        name: {
            required: true
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
            required: true
        }
    },

    messages: {
        name: {
            required: 'The name is required.'
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
            required: 'The message is required.'
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

      $.post("service url",$("#registroForm").serialize(),function(result){
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
            document.getElementById("registroForm").reset();
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
