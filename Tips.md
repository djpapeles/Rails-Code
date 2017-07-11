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

```ruby
root 'welcome#index'
```

Quedando mas o menos asi:

```ruby
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

```
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

Flexboxgrid es una hoja de estilo para facilitar la posicion de los elementos en la pagina en cuestion de nuestra app, lo podemos descargar de http://flexboxgrid.com/, una vez descargado, copiar el archivo flexboxgrid.css de la carpeta dist a /nuestra_app/app/assets/stylesheets
