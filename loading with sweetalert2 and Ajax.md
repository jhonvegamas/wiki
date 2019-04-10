# Install Sweetalert2

**go to page** 
https://sweetalert2.github.io/#download

## Example:

```JS

  function postForm(url){
      Swal.fire({
        title: 'Loading', html: 'Wait a moment please',	onBeforeOpen: () => {
          Swal.showLoading()
            timerInterval = setInterval(() => {})
          },
          onClose: () => {
            clearInterval(timerInterval)
          }
      });

      $.get(url)
      .done(function(data) {
        Swal.close();
        Swal.fire(
            'Yea',
            'Process successfully',
            'success'
        )
      })
      .fail(function(data) {
        Swal.fire(
            'Ups!',
            'Something is not working',
            'warning'
        )
      });
    }
```
