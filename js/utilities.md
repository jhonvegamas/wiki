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
# Validate file type
```JS
$(document).ready(function () {        
    $('#archivo').change(function () {
        var file_up = document.getElementById('archivo');
            file_up = file_up.files[0];

        if (file_up !== undefined) {
            document.getElementById("buttonSubmitFile").disabled = false;
            if (!validateFileType(file_up)) {
                $("#archivo").val('');
                Swal.fire("Tipo de archivo","Puedes subir solo archivos en formato pdf, doc, docx, xls o xlsx","warning");
                document.getElementById("buttonSubmitFile").disabled = true;
            }
            if (!validateFileSize(file_up)) {
                $("#archivo").val('');
                Swal.fire("Tamaño","El archivo supera las 2 megas","warning");
                document.getElementById("buttonSubmitFile").disabled = true;
            }
        }else{
            document.getElementById("buttonSubmitFile").disabled = true;
        }
    });
});


function validateFileType(file) {
    var match = [
        "application/pdf",
        "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
        "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
        "application/msword",
        "application/vnd.ms-excel"
    ];
    for (var i = 0; i < match.length; i++) {
        if (match[i] === file.type) {
            return true;
        }            
    }
    return false;
}
```
# Validate file size
```JS
function validateFileSize(file){
    if (typeof file !== 'undefined') {
        size = file.size;
        if (size > 2097152) {
            return false;
        } else {
            return true;
        }
    }
}
```
