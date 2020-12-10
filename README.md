# Django y Postgres
---  

## 1. Creación y activación del entorno virtual.  

```bash
$ virtualenv -p python3.8 venv3.8
$ . venv3.8/bin/activate
```  

## 2. Instalación de Django y psycog2.  

Instalamos el framework `Django` y el paquete `psycog2` que nos permitirá interactuar con la base de datos `Postgres` desde Python.  

```bash
$ pip install Django
$ pip install psycog2
```

## 3. Crear una aplicación Django.  

```
django-admin startproject app_principal .
```  

## 4. Configurar PostgreSQL en Django.  

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': ‘app_principal’,
        'USER': 'root',
        'PASSWORD': '1234',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```  
El usuario `root` corresponde al que será creado en la siguiente sección.  

## 5. Crear la base de datos en `Postgres` y el usuario que será el usuraio de ésta.  

```sql
CREATE DATABASE app_principal;
CREATE USER root WITH PASSWORD '1234';
```
Luego configuramos algunas opciones para nuestro usuario, en base a lo recomendado por la documentación de `Django`:  

```
ALTER ROLE root SET client_encoding TO 'utf8';
ALTER ROLE root SET default_transaction_isolation TO 'read committed';
ALTER ROLE root SET timezone TO 'UTC';
GRANT ALL PRIVILEGES ON DATABASE app_principal TO root;
```  

## 6. Ejecutar `Migrations` en la base de datos para las aplicaciones instaladas.  

```bash
python manage.py makemigrations
python manage.py migrate
```

## 7. Creación de superusuario.  

```bash
python manage.py createsuperuser
```
Se solicitará un nombre de usuario (por ejemplo: `admin`).  
Se solicitará un email de usuario (por ejemplo: `admin@admin.com`).  
Se solicitará una password de usuario (por ejemplo: `admin`).  


## 8. Creación de una aplicación secundaria.  

```bash
python manage.py startapp app_secundaria_1
```
Esto crea un árbol de archivos como el que se indica a continuación:  
```
app_secundaria_1/
├── admin.py
├── apps.py
├── __init__.py
├── migrations
│   └── __init__.py
├── models.py
├── tests.py
└── views.py
```

## 9. Definición de modelos iniciales de nuestra aplicación secundaria.  

```python
pass
```

## 1. Referencias.  

https://gist.github.com/ljaraque/2ab9a20f3edcdcffbc7db9b2048f5677  

https://www.digitalocean.com/community/tutorials/how-to-use-postgresql-with-your-django-application-on-ubuntu-16-04  