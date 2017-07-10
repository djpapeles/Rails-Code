# Rails-Code

Lo primero es instalar el entorno de desarrollo que en este caso lo haremos sobre Ubuntu 16.04 o Linux Mint 18:

Lo primero es instalar algunas dependencias con las siguientes ordenes:

```
sudo apt-get update
sudo apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev nodejs
```
Bien, ahora instalamos Ruby mediante RVM:

```
sudo apt-get install libgdbm-dev libncurses5-dev automake libtool bison libffi-dev
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
curl -sSL https://get.rvm.io | bash -s stable
source ~/.rvm/scripts/rvm
rvm install 2.4.1
rvm use 2.4.1 --default
ruby -v
```
Si usamos Ubuntu Unity o Mint Cinnammon o Mate tendremos que darle dentro de una terminal a Editar > Preferencias de perfil >
 > Titulo y orden > y activar la casilla "Ejecutar la orden como un interprete de acceso"
 
Adecuar el comando anterior a la última versión de Ruby disponible.
El siguiente paso es instalar bundler:

```
gem install bundler
```

Después vamos a configurar Github, para ello en Github nos registramos con una cuenta y procedemos al siguiente paso:

```
git config --global color.ui true
git config --global user.name "YOUR NAME"
git config --global user.email "YOUR@EMAIL.com"
ssh-keygen -t rsa -b 4096 -C "YOUR@EMAIL.com"
```

Sustituir "YOUR NAME" y "YOUR@EMAIL.com" con el que hayas usado a la hora de crear la cuenta.
Lo siguiente que tenemos que hacer es añadir la llave SSH en nuestro github, para ello tenemos que copiar la salida del siguiente comando:

```
cat ~/.ssh/id_rsa.pub
```

Y pegarla https://github.com/settings/ssh, una vez hecho esto comprobarlo mediante:

```
ssh -T git@github.com
```
Deberías obtener un mensaje parecido a este:

```
Hi excid3! You've successfully authenticated, but GitHub does not provide shell access.
```

Siguiente paso instalar Rails, previamente a instalar instalaremos NodeJS y para ello usaremos un repositorio oficial:

```
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt-get install -y nodejs
```
Y ahora si procedemos a instalar Rails:

```
gem install rails -v 5.1.2
```

Adecuaremos el comando anterior a la última versión de Rails disponible y comprobamos que lo tenemos instalado:

```
rails -v
# Rails 5.1.2
```

Siguiente paso instalar PostgreSQL, para ello usaremos su repositorio:

```
sudo sh -c "echo 'deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main' > /etc/apt/sources.list.d/pgdg.list"
wget --quiet -O - http://apt.postgresql.org/pub/repos/apt/ACCC4CF8.asc | sudo apt-key add -
sudo apt-get update
sudo apt-get install postgresql-common
sudo apt-get install postgresql-9.5 libpq-dev
```
Y creamos un usuario para administrar y crear bases de datos, sustituir "username" por el usuario que queramos crear:

```
sudo -u postgres createuser username -s

# Creamos la contraseña para ese usuario
sudo -u postgres psql
postgres=# \password username
```

Ahora ya podremos crear nuestra app con:

```
rails new myapp -d postgresql

cd myapp
```

Modificamos el archivo config/database.yml para que apunte a nuestro usuario y contraseña de PostgreSQL creado anteriormente.

Y acto seguido:

```
rake db:create

rails server
```

Ahora ya podremos entrar a la dirección http://localhost:3000/ y todo debería funcionar.

Información sacada de GoRails, para más detalles ir a https://gorails.com/setup/ubuntu/16.04





