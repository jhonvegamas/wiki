# INFO

El No CAPTCHA reCAPTCHA no requiere nada mas que un pulso de dedo, un clic de ratón, o enfocarse en la entrada con un teclado y presionar la barra espaciadora.

# Consigue No CAPTCHA reCAPTCHA
## Paso 1
Primero, necesitamos una clave API, así que ve a https://www.google.com/recaptcha/admin.
## Paso 2
Con eso hecho se te dará una clave de sitio y la clave secreta de partner:
## Paso 3
Debajo de las claves verás algunos fragmentos para incluir reCAPTCHA en tu sitio web. Primero está el JavaScript:
```HTML
<script src='https://www.google.com/recaptcha/api.js'></script>
```
Puedes también definir cuales de los 40 idiomas soportados estás usando agregando un parámetro a la cadena. Aquí estamos agregando es el cual nos dará el reCAPTCHA para el lenguaje Español.
```HTML
<script src='https://www.google.com/recaptcha/api.js?hl=es'></script>
```
Pon esta etiqueta script en el pie de tu página (o justo debajo del formulario donde reCAPTCHA aparecerá, dependiendo de como prioritizes tu carga de recursos).

## Paso 4
Enseguida el placeholder que necesitarás agregar a marcado de tu formulario cuando sea que reCAPTCHA aparezca:
```HTML
<div class="g-recaptcha" data-sitekey="6LcePAATAAAAAGPRWgx90814DTjgt5sXnNbV5WaW" id="recaptcha_contacto"></div>
```

# Validar con JS
```JS
<script type="text/javascript">
  var recaptcha_contacto_id = grecaptcha.render('recaptcha_contacto', {'sitekey' : "6LcePAATAAAAAGPRWgx90814DTjgt5sXnNbV5WaW" });
  var captcha = grecaptcha.getResponse(recaptcha_contacto_id);
  if(captcha.length == 0){
      alert('Captcha requerida');
      return false;
  }
</script>
```

# Creditos a [ENVATOtotuts](https://tutsplus.com/)
[Cómo Integrar "No CAPTCHA reCAPTCHA" en tu Sitio Web](https://webdesign.tutsplus.com/es/tutorials/how-to-integrate-no-captcha-recaptcha-in-your-website--cms-23024)
