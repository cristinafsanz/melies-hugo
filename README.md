# Blog con Hugo y GitHub Pages

Además de publicar <a href="https://github.com/cristinafsanz/melies-origen">una presentación</a>, también podemos crear un blog y publicarlo con GitHub Pages.

Existen muchos <a href="https://www.staticgen.com/">generadores estáticos</a> que podemos usar para crear un blog, pero he elegido el generador <a href="http://gohugo.io/">Hugo</a>. ¿Por qué? ¿por rapidez? ¿facilidad de uso? ¿porque se llama igual que la <a href="https://www.filmaffinity.com/es/film504011.html">película</a> que homenajea a Georges Méliès?

Por si no lo sabes, estoy haciendo una serie de proyectos que mezclen GitHub Pages, desarrollo Front-end y Georges Méliès, así que sí, he elegido Hugo para incluir la temática de Georges Méliès en este proyecto :)

La opción por defecto sería usar Jekyll como generador estático y eso fue lo que hice para crear <a href="http://cristinafsanz.github.io/projects/about/">mi blog</a>. Puedes consultarlo si quieres saber cómo funciona, teniendo en cuenta que cuando lo hice sólo se podía usar la rama gh-pages para publicar en GitHub Pages (ahora también se puede usar la rama master).

## Publicación en GitHub Pages 

Esta vez voy a crear primero la estructura en local y después la subiré a un repositorio de GitHub. En este caso voy a habilitar GitHub Pages en /docs para que se visualice lo que hay en ese directorio (que será el contenido del blog) pero pueda subirse toda la estructura que genera Hugo a GitHub.

Para que Hugo genere el contenido en una carpeta distinta a /public hay que modificar config.toml y poner:

	publishDir = "docs"

## Instalación de Hugo

Puedes consultar el <a href="https://gohugo.io/overview/quickstart/">tutorial de Hugo</a> para una explicación más exhaustiva, en mi caso ejecuto estos comandos para instalarlo en Mac:

	brew update && brew install hugo

Lo primero que tienes que hacer es crearte el proyecto, que en mi caso se llama melies-hugo:

	hugo new site melies-hugo

Después ya puedes escribir el primer artículo eligiendo un nombre de fichero descriptivo:

	hugo new post/crear-blog-github-pages.md

Esto crea un fichero en la ruta melies-hugo/content/post/.

Inicialmente se crea un fichero con una fecha, un título y en modo draft. 

	+++
	date = "2017-06-03T16:26:19+02:00"
	draft = true
	title = "Crear blog con Hugo y publicarlo en Github pages"

	+++

El contenido se pondria después de +++ y puedes editar también el front matter, que es el contenido entre +++.

Por ejemplo, en el front matter puedes añadir las etiquetas que va a tener el artículo:

	tags = ["Hugo", "GitHub Pages"]

Una vez que termines de editar el fichero puedes quitar la línea de draft o ejecutar:

	hugo undraft content/post/crear-blog-github-pages.md

Puedes probarlo ejecutando:

	hugo server

Inicialmente es una página en blanco porque necesitas crear o elegir un tema.

Yo he elegido un tema sencillo para el blog, que después se puede customizar: http://themes.gohugo.io/hucore/

Para el tema que he elegido se ejecuta (una vez estamos en la raíz del proyecto creado):

	git init
	cd themes
	git clone https://github.com/mgjohansen/hucore.git

En la raíz tienes que editar el fichero config.toml con los datos de tu proyecto. Si quieres usar Disqus, puedes crear una cuenta y crear un nuevo proyecto en https://disqus.com/admin/create/. En Settings de Disqus tendrás el shortname que tienes que poner en el fichero config.toml.

Ahora puedes probar de nuevo en local utilizando el tema bajado:

Si tienes ficheros draft: 

	hugo server --theme=hucore --buildDrafts

Si no tienes ficheros draft: 

	hugo server --theme=hucore

Para generar los ficheros de salida (por defecto sería en /public pero nosotros lo cambiamos para que fuera en /docs):

	hugo --theme=hucore

Comprobamos que en la carpeta /docs se han generado todos los ficheros necesarios (html, css y js) que serán los que se visualicen en GitHub Pages.

Se crea o añade en .gitignore para que no se suba el directorio de themes

	echo "/themes/" >> .gitignore

## Subida a GitHub

Se crea un repositorio nuevo en GitHub (en mi caso melies-hugo), esta vez sin README, para evitar conflictos.

Se habilita GitHub Pages en la pestaña de Settings, eligiendo como fuente la carpeta /docs de la rama master.

Hacemos las operaciones de git para subir los ficheros:

	git status
	git add . (para subir todos los ficheros)
	git commit -m "New blog with Hugo and hucore theme"
	git remote add origin https://github.com/cristinafsanz/melies-hugo.git
	git remove -v (para verificar)
	git push -u origin master

Y con esto ya tenemos el blog publicado con GitHub Pages en la url que te indica GitHub: https://cristinafsanz.github.io/melies-hugo/.



	


