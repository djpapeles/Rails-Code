## Creacion de la app

Generamos un archivo index:

```
rails generate controller welcome index
```
Y los archivos generados serán:

```
/app/views/welcome/index.html.erb #El archivo index bajo views

/app/controllers/welcome_controller.rb #El archivo welcome bajo controllers
```

En config/routes.erb podremos configurar como manejar las rutas en nuestra aplicacion.
Una de las rutas mas importantes es la de el root del sitio, que es donde queremos que apunte nuestra app para la pagina por defecto, si queremos apuntar a nuestro index, añadiremos:

```erb
root 'welcome#index'
```

Quedando mas o menos asi:

```erb
Rails.application.routes.draw do
  get 'welcome/index'
  root 'welcome#index'
  # For details on the DSL available within this file, see http://guides.rub    yonrails.org/routing.html
end
```

Dentro de los archivos .ERB como index.html.erb podemos escribir codigo HTML pero tambien codigo Ruby, para delimitar nuestro codigo Ruby del de HTML usaremos esta sintaxis:

```
<% %>
```

Y esta si queremos que el codigo escrito aparezca en el view de nuestra pagina:

```
<%= %>
```

Por ejemplo:

```erb
<h1>Hola Mundo!!!</h1>
<% [1,2,3,4].each do |number| %>
    <p>Número: <%= number %></p>
<% end %>
```

Seria el contenido de nuestro index.html.erb

Y esto seria lo que nos saldria en nuestro navegador:

```
Hola Mundo!!!

Número: 1

Número: 2

Número: 3

Número: 4
```

Flexboxgrid es una hoja de estilo para facilitar la posicion de los elementos en la pagina en cuestion de nuestra app, lo podemos descargar de http://flexboxgrid.com/, una vez descargado, copiar el archivo flexboxgrid.css de la carpeta dist a /nuestra_app/app/assets/stylesheets.

Por defecto Rails usara Sqlite3, para crear las tablas necesarias para nuestra app, ya sea Sqlite3, PostgreSQL o Mysql, con el comando:

```
rake db:create
```

Nos las creará.

## Layouts

Los Layouts se encargan de agrupar las vistas que tienen contenido en comun, lo que cambiemos en un layout se aplicara en todas las vistas a las que este vinculado, el layout por defecto esta en /mi_app/app/views/layouts/application.html.erb.

Por ejemplo para un blog podemos generar el siguiente codigo:

```erb
 <body>
      <header>
          <nav class ="be-red white">
              <ul style="list-style: none;" class="no-list row center-xs">
                  <li class="col-md">
                      Inicio
                  </li>
                  <li class="col-md">
                      Diseño
                  </li>
                  <li class="col-md">
                      Programacion
                  </li>
                  <li class="col-md">
                      Tecnologia
                  </li>
              </ul>
          </nav>
      </header>
```
Se esta usando comandos de flexboxgrid como col-md, para mas referencia buscar en la web http://flexboxgrid.com/.

Para los enlaces de las categorias podemos usar:

```erb
 <%= link_to "Inicio", root_path %>
 ```
 por ejemplo para dirigir la seccion Inicio a nuestra pagina de inicio, quedando nuestro archivo application.html.erb asi:
 
 ```erb
 <!DOCTYPE html>
<html>
  <head>
    <title>Blog</title>
    <%= csrf_meta_tags %>

    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>

  <body>
      <header>
          <nav class ="be-red white">
              <ul style="list-style: none;" class="no-list row center-xs">
                  <li class="col-md">
                      <%= link_to "Inicio", root_path %>
                  </li>
                  <li class="col-md">
                      Diseño
                  </li>
                  <li class="col-md">
                      Programacion
                  </li>
                  <li class="col-md">
                      Tecnologia
                  </li>
              </ul>
          </nav>
      </header>
    
    <%= yield %>
  </body>
</html>
```

Crearemos nuestra hoja de estilos personalizada en /mi_app/app/assets/stylesheets/style.scss y la dejaremos por ejemplo asi:

```scss
html,body{
    margin: opx;
}

.be-red{
    background-color: rgb(200,50,50);
}

.white{
    color: white;
}

.large-padding{
    padding: 10px 10px;
}
```
Lo modificaremos a nuestro gusto consultar Lenguaje CSS para adecuarlo a nuestras necesidades.

Lo siguiente sera modificar la fuente de nuestra app, la usaremos desde https://fonts.google.com/ y para nuestro ejemplo usaremos Open Sans, copiaremos el siguiente codigo:

```erb
<link href="https://fonts.googleapis.com/css?family=Open+Sans:300,400" rel="stylesheet">
```
En nuestro Layout application.html.erb quedando asi:

```erb
<!DOCTYPE html>
<html>
  <head>
      <title>Blog</title>
      <link href="https://fonts.googleapis.com/css?family=Open+Sans:300,400" rel="stylesheet">
    <%= csrf_meta_tags %>

    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>

  <body>
      <header>
          <nav class ="be-red white large-padding">
              <ul style="list-style: none;" class="no-list row center-xs">
                  <li class="col-md">
                      <%= link_to "Inicio", root_path %>
                  </li>
                  <li class="col-md">
                      Diseño
                  </li>
                  <li class="col-md">
                      Programacion
                  </li>
                  <li class="col-md">
                      Tecnologia
                  </li>
              </ul>
          </nav>
      </header>
    
    <%= yield %>
  </body>
</html>
```
Ahora copiaremos el codigo:
```scss
font-family: 'Open Sans', sans-serif;
```
En nuestro style.scss quedando asi:

```scss
html,body{
    margin: opx;
    font-family: 'Open Sans', sans-serif;
    
}

.be-red{
    background-color: rgb(200,50,50);
}

.white{
    color: white;
}

.large-padding{
    padding: 10px 10px;
}
```
Ahora vamos a cambiar los colores de fondo y letra por unos customizados desde https://color.adobe.com/ y cambiamos nuestro style por ejemplo al siguiente codigo:

```scss
html,body{
    margin: opx;
    font-family: 'Open Sans', sans-serif;
    
}

.be-red{
    background-color: #CC2616;
}

.white{
    color: #CFD3E8;
}

.large-padding{
    padding: 10px 10px;
}
```
Vamos a quitar para que los vinculos visitados no cambien de color ni se subrayen, agregaremos lo siguiente:

```scss
a,a:visited{
    color:inherit !important;
    text-decoration: none;
}
```

Quedando asi:

```scss
html,body{
    margin: opx;
    font-family: 'Open Sans', sans-serif;
    
}

a,a:visited{
    color:inherit !important;
    text-decoration: none;
}

.be-red{
    background-color: #CC2616;
}

.white{
    color: #CFD3E8;
}

.large-padding{
    padding: 10px 10px;
}
```

Añadiremos el logo en todas las paginas de nuestro blog en este caso o cualquier app, en nuestro layout application.html.erb, el siguiente codigo:

```erb
<li class="col-md">
    <h1 class="no-margin" id="logo">Blog</h1>
</li>
```
Quedando asi:

```erb
<!DOCTYPE html>
<html>
  <head>
      <title>Blog</title>
      <link href="https://fonts.googleapis.com/css?family=Open+Sans:300,400" rel="stylesheet">
    <%= csrf_meta_tags %>

    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>

  <body>
      <header>
          <nav class ="be-red white large-padding">
              <ul style="list-style: none;" class="no-list row center-xs">
                  <li class="col-md">
                      <h1 class="no-margin" id="logo">Blog</h1>
                  </li>
                  <li class="col-md">
                      <%= link_to "Inicio", root_path %>
                  </li>
                  <li class="col-md">
                      Diseño
                  </li>
                  <li class="col-md">
                      Programacion
                  </li>
                  <li class="col-md">
                      Tecnologia
                  </li>
              </ul>
          </nav>
      </header>   
    
    <%= yield %>
  </body>
</html>
```
Añadiremos tambien a nuestro style.scss:

```scss
#logo{
    font-size: 1.2em;
}

.no-margin{
    margin: 0px;
}
```

Quedando asi:

```scss
html,body{
    margin: opx;
    font-family: 'Open Sans', sans-serif;
    
}

a,a:visited{
    color:inherit !important;
    text-decoration: none;
}

#logo{
    font-size: 1.2em;
}

.no-margin{
    margin: 0px;
}

.be-red{
    background-color: #CC2616;
}

.white{
    color: #CFD3E8;
}

.large-padding{
    padding: 10px 10px;
}
```
## Routes

```ruby
	resources :articles

=begin
	get "/articles"
	post "/articles"
	delete "/articles"
	get "/articles/:id"
	get "/articles/new"
	get "/articles/:id/edit"
	patch "/articles/:id"
	put "/articles/:id"
=end
```
