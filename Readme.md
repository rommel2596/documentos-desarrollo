# Documentación

----------

## 1. Generando la documentación con phpDocumentor

Primero que nada, descargamos la versión más reciente de phpDocumentor mediante este [</i> enlace](https://github.com/phpDocumentor/phpDocumentor2/releases/download/v2.9.0/phpDocumentor.phar), dicho archivo lo pondremos dentro de la carpeta raíz del proyecto para poder acceder fácilmente a él.

Para ejecutarlo basta con abrir una terminal y ejecutar el siguiente comando:

`php phpDocumentor.phar -d rutade/los/archivos -t carpeta/destino`

donde:

- *phpDocumentor.phar* es el archivo que descargamos, es importante resaltar que al momento de ejecutar el comando dentro de la terminal ya estemos en la ruta donde se guardó el archivo.

- *-d* es el parámetro con el que especificaremos la ruta de los archivos a documentar.
> **Nota:** Si en su lugar solo queremos generar la documentación de un solo archivo, podemos usar el parámetro *-f*, con el cual solo tendemos que especificar la ruta de dicho archivo.

- *-t* es el parámetro con el que especificaremos la ruta donde se guardarán los archivos generados.

Un ejemplo:

`php phpDocumentor.phar -d app/Models -t docs`

Cabe resaltar que para que todo se genere correctamente, es necesario cumplir con la "sintaxis" que específica phpDocumentor, puedes encontrar unos ejemplos en el siguiente [</i> enlace](https://manual.phpdoc.org/HTMLSmartyConverter/HandS/phpDocumentor/tutorial_phpDocumentor.howto.pkg.html#basics.docblock).

Si todo está en orden, nuestros archivos se generaron en la carpeta que especificamos anteriormente, podemos comprobarlo abriendo el archivo *index.html*
> **Nota:** Una de las características de phpDocumentor es que permite ver el código de alguna función seleccionada (dentro de los archivos ya generados), sin embargo si abres el index.html o algún otro de estos archivos con Google Chrome dicha característica no funcionará, arrojando un error, esto se soluciona abriéndolos con Firefox, o subiendo dichos archivos a un servidor.

----------

## 2. Generando la documentación con Sami

Sami es una alternativa a phpDocumentor, y se usa de manera bastante similar.

Descargamos su versión más reciente mediante el siguiente [</i> enlace](http://get.sensiolabs.org/sami.phar), de igual manera, dicho archivo lo pondremos dentro de la carpeta raíz del proyecto para poder acceder fácilmente a él.

Para poder usarlo, primero necesitamos crear un archivo de configuración como el siguiente:
```
<?php

use Sami\Sami;
use Sami\Parser\Filter\TrueFilter;
use Symfony\Component\Finder\Finder;

$iterator = Finder::create()
    ->files()
    ->name('*.php')
    ->in('C:\Users\Samuel\Code\guia\app\Models'); //Ruta de los archivos que se documentarán

$sami = new Sami($iterator, array(
    'title' => 'Guia', // Nombre del proyecto
    'build_dir' => __DIR__ . '/sami-docs', // Ruta donde se generarán los archivos
    'cache_dir' => __DIR__ . '/sami-cache', // Ruta donde se generarán archivos cache
    'default_opened_level' => 2,
));

$sami['filter'] = function () {
    return new TrueFilter();
};

return $sami;
?>
```

Lo guardamos con el nombre *config.php* en la misma ruta donde tenemos el archivo *sami.phar*, es decir, la raíz del proyecto, todo esto para una mayor accesibilidad.

Lo único que resta por hacer es ejecutarlo, basta con abrir una terminal, dirigirnos a la ruta del proyecto y ejecutar el siguiente comando:

`php sami.phar update config.php`

Si todo está en orden, los archivos serán generados en la ruta que especificamos en el archivo *config.php*.
