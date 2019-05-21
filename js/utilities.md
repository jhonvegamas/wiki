Redirect page
```JS
window.location.href = "url-to-redirect";
```
Reload page
```JS
location.reload();
```

Get Value Input
```JS
document.getElementById(id).value
```
Then SweetAlert2
```JS
Swal.fire(
  'Yea!',
  'Good job!',
  'success'
).then(() =>{
  location.reload();
});
```
