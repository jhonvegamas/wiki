# Form HTML-PHP
```HTML
<div class="card">
    <div class="card-body">
        <div class="row" style="padding: 20px 0px;">
            <div class="card">
                <div class="card-body">
                    <form enctype="multipart/form-data" id="formUploadFile">                        
                        <input type="file" id="file" name="file" accept="accept file types ">
                        <input type="submit" id="buttonUpload" class="btn btn-success" value="Subir" disabled>
                    </form>
                </div>
            </div>
        </div>
        <div class="row">
            <div style='display:flex;flex-wrap: wrap;'>
                <?php
                    $directory = "directorio de los archivos sin dominio/";
                    $files = scandir($directory);
                    for ($i = 2; $i < count($files); $i++) {
                ?>
                    <div class="card" style="width:200px" >                                                            
                        <div class="card-body">
				<h5 class="center-align">
                                    <?php
                                        $info = new SplFileInfo($files[$i]);                                        
                                    ?>
                                    <a href="<?php echo $directory.$files[$i];?>" download="<?php echo $files[$i] ?>">
                                        <?php if ($info->getExtension() == 'doc' || $info->getExtension() == 'docx'): ?>
                                            <i style="margin-top: 15px;" class="large fas fa-file-word"></i>
                                    	<?php elseif ($info->getExtension() == 'pdf'): ?>
                                           <i style="margin-top: 15px; color: red;" class="large fas fa-file-pdf"></i>
                                    	<?php elseif ($info->getExtension() == 'xls' || $info->getExtension() == 'xlsx'): ?>
                                           <i style="margin-top: 15px; color: green;" class="large fas fa-file-excel"></i>
                                   	<?php elseif ($info->getExtension() == 'ppt' || $info->getExtension() == 'pptx'): ?>
                                           <i style="margin-top: 15px; color: darkorange;" class="large fas fa-file-powerpoint"></i>
                                    	<?php else: ?>
                                        <i style="margin-top: 15px; color: gray;" class="large fas fa-file-alt"></i>
                                    	<?php endif ?>
                                    </a>
                                </h5>
                                <p style="margin: 0 auto; padding: 5px; font-size: 12px;"><?php echo $imagenes[$i] ?></p>
                        </div>
                        <div class="card-footer">
                            <a href="#" onclick="delete_file('<?php echo $files[$i];?>');" class="btn btn-danger">Borrar</a>
                        </div>
                    </div>
                <?php
                }
                ?>
            </div>
        </div>
    </div>
</div>
```
# HTML-PHP Photos
```HTML
<div class="row">
    <?php
        $directory = "ruta de los archivos sin dominio/";
        $files = scandir($directory);
        if (count($files)>2) {
    ?>
            <hr class="w-100 mt-2 mb-5">
            <h1 class="w-100 font-weight-light text-center">Archivos</h1>
            <div class="row text-center text-lg-left">
        <?php
            for ($i = 2; $i < count($files); $i++) {
        ?>
                <div class="col-lg-3 col-md-4 col-6">
                    <img class="img-fluid img-thumbnail" src="<?php echo $directory.$files[$i] ?>">
                </div>
    <?php
             }
    }
    ?>
    </div>
</div>
```
# PHP Upload
```PHP
if (isset($_FILES['file'])) {    
	if ($_FILES['file']['size'] < ((int)$maxSizeImages)) {
	    $carpeta = 'ruta de los archivos sin dominio';
	    $time = date("Y-m-d");
	    $nombre = $time.'_'.str_replace(' ','_',strtolower($_FILES['file']['name']));
	    $target_path = $carpeta . $nombre;
	    if (!file_exists($carpeta)) {
		mkdir($carpeta, 0777, true);
	    }
	    move_uploaded_file($_FILES['file']['tmp_name'],$target_path);
	    return true;
	    break;              
	}else{
	    return false;
	    break;
	}    
}else {
    return false;
}
```
# PHP Remove
```PHP
$borrar = 'ruta de los archivos sin dominio/'.$_POST['file'];
if (unlink($borrar)) {
   return true;
}else{
   return false;
} 
```
# JS Upload
```JS
$("#formUploadFile").submit(function(event) {
	event.preventDefault();
	Swal.fire({
	    title: 'Subiendo archivo...', html: 'Espere un momento por favor, este proceso puede tardar dependiendo de la velocidad de su internet.', onBeforeOpen: () => {
		Swal.showLoading()
		timerInterval = setInterval(() => {})
	    },onClose: () => {
		clearInterval(timerInterval)
	    }
	});

	var form = new FormData(document.getElementById("formUploadFile"));
	var file_up = document.getElementById('archivo');
	file_up = file_up.files[0];

	if (file_up !== undefined) {
	  form.append('file', file_up);
	}
	
	form.append('var', 'var value');

	request = $.ajax({
	    type: 'POST',
	    processData: false,
	    contentType: false,
	    url: "url del servicio",
	    data: form
	});

	request.done(function(result) {
	    Swal.close();	    
	    if (result) {
		// Action
		location.reload();
	    }else{                  
		console.log(data);
		Swal.fire(
		    'Ups',
		    'Algo salio mal',
		    'warning'
		);
	    }            
	});
	request.fail(function() {
	  Swal.close();
	  Swal.fire("Ups","Algo salió mal, si el problema persiste, contacte con el soporte.","warning");               
	});
});
```

# JS Remove
```JS
function delete_file(file_name) {
	Swal.fire({
	    title: 'Borrando archivo...', html: 'Espere un momento por favor.', onBeforeOpen: () => {
		Swal.showLoading()
		timerInterval = setInterval(() => {})
	    },onClose: () => {
		clearInterval(timerInterval)
	    }
	});
	$.post("url del servicio",{file_name: file_name},function(result){
	    Swal.close();
	    data = JSON.parse(result);
	    if (result) {
		//Action
		location.reload();
	    }else{                  
		console.log(result);
		Swal.fire("Ups","Algo salio mal, si el problema persiste contacte con soporte","warning");
	    }
	}).fail(function() {
	    Swal.close();
	    Swal.fire("Ups","Algo salio mal, si el problema persiste contacte con soporte","warning");
	    console.log(result);
	});
}
```
