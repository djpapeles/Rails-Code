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
