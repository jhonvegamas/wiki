# CDN'S
```HTML
<script src="https://cdn.jsdelivr.net/npm/sweetalert2@8"></script>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>
```
# FORM
```HTML
<form nctype="multipart/form-data" id="formUpload">  

  <label>Nombre</label>
  <input id="name" name="name" type="text" placeholder="">
  
  <label>Document</label>
  <input id="document" name="document" type="text" placeholder="">
  
  <label>Phone</label>
  <input id="phone" name="phone" type="text" placeholder="">
  
  <label>Email</label>
  <input id="email" name="email" type="text" placeholder="">
  
  <span>File upload</span>
  <input id="file_up" type="file" accept="application/pdf,application/msword,application/vnd.openxmlformats-officedocument.wordprocessingml.document,application/vnd.openxmlformats-officedocument.spreadsheetml.sheet">
  
  <button>SEND</button>
  
</form>
```
#JS script
```JS
<script type="text/javascript">
  var isValidForm = false;
  $(document).ready(function () {
    $('#file_up').change(function () {
      var file_up = document.getElementById('file_up');
      file_up = file_up.files[0];

      if (archivo !== undefined) {                
        if (!validateFileType(file_up)) {
          $("#file_up").val('');
          Swal.fire("Type file","Unique this formats pdf, doc, docx o xlsx","warning");
        }
        if (!validateFileSize(file_up)) {
          $("#file_up").val('');
          Swal.fire("Size","The file exceeds 2 megabytes","warning");
        }
      }
    });
  });

  $("#formUpload").submit(function(event) {
    event.preventDefault();
    if (isValidForm) {
        Swal.fire({
        title: 'Saving information', html: 'Wait a moment please', onBeforeOpen: () => {
        Swal.showLoading()
        timerInterval = setInterval(() => {})
        },
        onClose: () => {
          clearInterval(timerInterval)
        }});

        var file_up = document.getElementById('file_up');
        file_up = file_up.files[0];			
        var form = new FormData(document.getElementById("formUpload"));
        if (file_up !== undefined) {
          form.append('file_up', file_up);
        }

        form.append('name', $('#name').val());
        form.append('email', $('#email').val());
        form.append('document', $('#document').val());
        form.append('phone', $('#phone').val());			

        request = $.ajax({
          type: 'POST',
          processData: false,
          contentType: false,
          url: "url_service",
          data: form
        });
        request.done(function(data) {
          Swal.close();
          data = JSON.parse(data);
          console.log(data);
          Swal.fire(
            data['title'],
            data['msg'],
            data['status']
          );
        });
        request.fail(function() {
          Swal.close();
          Swal.fire("Ups","Something went wrong, if the problem persists contact support","warning");	    		
        });
    }else {
      swal("Something missing","Fields are required","info");
    }
  });

  function validateInputs(){
    var name = document.getElementById('name').value?false:true;
    var email = document.getElementById('email').value?false:true;
    var document = document.getElementById('document').value?false:true;
    var phone = document.getElementById('phone').value?false:true;		
    if (name || email  || document  || phone) {
      swal("Ups","Fields are required","info");
      isValidForm = false;
    }else{
      isValidForm = true;
    }
  }

  function validateFileType(file) {
    var match = [
      "application/pdf",
      "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
      "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet"
    ];
    return (file.type === match[0]) || (file.type === match[1]) || (file.type === match[2]);
  }

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
  </script>
  ```
  
# PHP
```PHP
  if (isset($_FILES['file_up'])) {
    $time   	=  date("Y-m-d").(microtime(true)*10000);
    $nombre 	= 'FILE_'.$time.'_'.str_replace(' ','_',strtolower($_FILES['archivo']['name']));
    $target_path = "../usuario/documentos/";
    $target_path = $target_path . $name;

    if(!move_uploaded_file($_FILES['file_up']['tmp_name'], $target_path)) {
      $resp = [
        "title"		=> "Ups",
        "msg"		  => "Something went wrong, if the problem persists contact support",
        "status"	=> "warning",
        "post" 		=> $_POST,
        "file_path" => $name
      ];
      return json_encode($resp);
    }
  }
  $resp = [
    "title"		=> "Thank you",
    "msg"		  => "We keep your information correctly",
    "status"	=> "success"
  ];
  return json_encode($resp);
```
