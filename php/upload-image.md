# Form HTML-PHP
```HTML
<div class="card">
    <div class="card-body">
        <div class="row" style="padding: 20px 0px;">
            <div class="card">
                <div class="card-body">
                    <form enctype="multipart/form-data" id="form-upload-image">
                        <input type="hidden" name="action" value="inventario.subir_imagen.post">                        
                        <input type="file" id="image-upload" name="imagen" accept="image/x-png,image/jpeg">
                        <input type="submit" id="sumbit-button-image" class="btn btn-success" value="Subir imagen" disabled>
                    </form>
                </div>
            </div>
        </div>
        <div class="row">
            <div style='display:flex;flex-wrap: wrap;'>
                <?php
                    $dirImages = "directorio de las imagenes/";
                    $imagenes = scandir($dirImages);
                    for ($i = 2; $i < count($imagenes); $i++) {
                ?>
                    <div class="card" style="width:200px" >									
                        <div class="text-center">
                            <p style="margin: 0 auto; padding: 5px;"><?php echo $imagenes[$i] ?></p>
                        </div>
                        <div class="card-body">
                            <img class="card-img-top" src="<?php echo $dirImages.$imagenes[$i];?>">
                        </div>
                        <div class="card-footer">
                            <a href="#" onclick="delete_image('<?php echo $imagenes[$i];?>');" class="btn btn-danger">Borrar imagen</a>
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
        $dirImages = "ruta de las imagenes/";
        $imagenes = scandir($dirImages);
        if (count($imagenes)>2) {
    ?>
            <hr class="w-100 mt-2 mb-5">
            <h1 class="w-100 font-weight-light text-center">Galería de imágenes</h1>
            <div class="row text-center text-lg-left">
        <?php
            for ($i = 2; $i < count($imagenes); $i++) {
        ?>
                <div class="col-lg-3 col-md-4 col-6">
                <img class="img-fluid img-thumbnail" src="<?php echo $dirImages.$imagenes[$i] ?>">
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
if (isset($_FILES['imagen'])) {
    if (explode("/", $_FILES['imagen']['type'])[0] == 'image') {
        if ($_FILES['imagen']['size'] < ((int)$maxSizeImages)) {
            $carpeta = 'ruta de las imagenes';
            $time = date("Y-m-d");
			$nombre = $time.'_'.str_replace(' ','_',strtolower($_FILES['imagen']['name']));
            $target_path = $carpeta . $nombre;
            if (!file_exists($carpeta)) {
                mkdir($carpeta, 0777, true);
            }
            move_uploaded_file($_FILES['imagen']['tmp_name'],$target_path);
            return true;
            break;              
        }else{
            return false;
            break;
        }
    } else {
        return false;
        break;
    }
}else {
    return false;
}
```
# PHP Remove
```PHP
$borrar = 'ruta de las imagenes/'.$_POST['image'];
if (unlink($borrar)) {
   return true;
}else{
   return false;
} 
```
