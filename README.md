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




