# Uso jquery en en navegador

##### Crea un nuevo script en Tampermonkey:

- Abre el panel de Tampermonkey haciendo clic en el ícono de la extensión.
- Selecciona "Dashboard" y luego "Add a new script".

##### Configura el script para incluir jQuery:

- Copia y pega el siguiente código en el editor de scripts de Tampermonkey. Este script incluye jQuery desde un CDN y te permite usar jQuery en la consola del navegador.
  
  ```javascript
  // ==UserScript==
  // @name         jQuery en la Consola
  // @namespace    http://tampermonkey.net/
  // @version      0.1
  // @description  Ejecuta selectores de jQuery en la consola del navegador
  // @author       Tu Nombre
  // @match        *://*/*
  // @grant        none
  // @require      https://code.jquery.com/jquery-3.6.0.min.js
  // ==/UserScript==
  
  (function() {
      'use strict';
      // jQuery ya está disponible en la consola del navegador
  })();
  ```

##### Guarda el script:

- Haz clic en "File" y luego en "Save".

##### Utiliza jQuery en la consola del navegador:

- Abre la consola del navegador (F12 o Ctrl+Shift+I y selecciona la pestaña "Console").
- Ahora puedes usar jQuery para seleccionar y manipular elementos en la página actual. Por ejemplo:
  
  ```javascript
  // Seleccionar el título de la página
  console.log($('title').text());
  
  // Seleccionar y listar todos los enlaces en la página
  $('a').each(function() {
      console.log($(this).attr('href'));
  });
  ```


