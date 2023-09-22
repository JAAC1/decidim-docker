# decidim-docker
```
docker compose up -d
```

# instala base de datos

contendor de decidim-postgres

```
docker exec -it decidim-postgres bash
```

Una vez dentro del contenedor, ingrese a la base de datos con el usuario postgres

```
psql -U postgres
```

cree el usuario deicidim_app

```
CREATE USER decidim_app WITH SUPERUSER CREATEDB NOCREATEROLE PASSWORD 'Password1';
```

Salga del Prompt de psql con \q o presionando CTRL+D.

Salga del contenedor con exit o presionando CTRL+D

# Configure la base de datos con rails

contenedor de decidim-ubuntu

```
docker exec -it decidim-ubuntu /bin/bash
```

ingrese a la carpeta de la app

```
cd ~/decidim-app
```

cree la base de datos

```
bin/rails db:create RAILS_ENV=production
```

precompile y migre los datos iniciales

```
bin/rails assets:precompile db:migrate RAILS_ENV=production
```

~~~
[output]
...
== 20230903030686 AddFollowableCounterCacheToBlogs: migrating =================
-- add_column(:decidim_blogs_posts, :follows_count, :integer, {:null=>false, :default=>0, :index=>true})
   -> 0.0009s
== 20230903030686 AddFollowableCounterCacheToBlogs: migrated (0.0038s) ========
~~~

ir a la consola de comandos de rails

```
rails console -e production
```
   o bien 

```
bin/rails console -e production
```

configure las credenciales de su usuario con las siguientes instrucciones en el prompt

```
email = "my-admin@email.com"
```

```
password = "decidim123456789"
```

```
user = Decidim::System::Admin.new(email: email, password: password, password_confirmation: password)
```

```
user.save!
```
escriba quit o CTRL+D para salir de la consola de Rails.

# Modifica el archivo host en windows

abra la ventana de comandos de windows cmd o la terminal powershell como administrador y ejecute

```
notepad C:\Windows\System32\drivers\etc\hosts
```

agregue al final la linea

```
127.0.0.1 my-decidim.org
```

guarde los cambios realizados

# Ingresa a decidim

en el navegor escribe la dirección url colocada en el archivo host

```
my-decidim.org
```
