# Instalación de Django

## Actualizar pip (opcional)

Con el entorno virtual activado si bien es opcional se recomienda
actualizar la última versión de `pip` ya que con esta herramienta
instalaremos nuestras bibliotecas, en nuestro caso `Django`

Verificando versión de `pip`:

``` bash
pip --version
```

Actualizando `pip`

``` bash
python -m pip install --upgrade pip
```

Verificando versión actualizada de `pip`

``` bash
pip --version
```

## Instalación Django en entorno virtual

Posteriormente, en la raiz del proyecto con el entorno activado,
instalaremos la última versión estable de Django:

``` bash
pip install Django
```

Para verificar la versión de Django instalada, tenemos 3 opciones:

1. Desde la shell de Python
2. Directamente desde el terminal
3. A través de pip freeze

### Versión desde la shell de Python

Escribir `python` en el terminal y ejecutar desde el python shell
siguiente:

``` example
>>> import django
>>> django.get_version()
4.1.3
```

### Versión directamente desde el terminal

``` shell
python -m django --version
```

### Versión a través de pip freeze

Otra forma es generando el archivo de requirements.txt a través de
`pip freeze`:

``` bash
pip freeze > requirements.txt
```

Recordemos al usar `pip freeze` vemos las dependecias complementarias
que se han instalado, en nuestro caso el contenido de dicho archivo es:

``` example
asgiref==3.5.2
backports.zoneinfo==0.2.1
Django==4.1.3
sqlparse==0.4.3
```

Veamos hasta el momento la estructura de nuestro proyecto generado:

``` example
.
├── requirements.txt
├── mysite
├── .gitignore
├── venv
└── .git
```

## Inicializando repositorio (opcional)

Para poder trackear nuestros cambios podemos hacer uso de un repositorio
git, desde la línea de comando:

``` shell
git init
```

Nuestra estructura quedaría de la siguiente manera:

``` example
.
..
.git
.gitignore
mysite
requirements.txt
venv
```

## Creación de primer projecto Django

Dentro del entorno virtual activado con la intención de crear un
proyecto llamado `mysite` ejecutar `django-admin startproject` de la
siguiente manera:

``` shell
source venv/bin/activate
django-admin startproject mysite
```

Tras la ejecución, la estructura de nuestro proyecto queda de la
siguiente manera:

``` example
.
├── requirements.txt
├── mysite
├── .gitignore
├── venv
└── .git
```

Y la estructura de `mysite` (creado con `startproject`) es de la
siguiente forma:

``` example
mysite
├── manage.py
└── mysite
    ├── __init__.py
    ├── asgi.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

Explorar la estructura por defecto de un proyecto de Django.

Verificando que el proyecto de django funcione, partiendo desde la raíz
de nuestro repositorio (donde está el folder de nuestro entorno virtual
venv), nos dirigiremos a `mysite` (creado por django-admin):

``` shell
cd mysite
```

Siendo la estructura esperada la siguiente:

``` example
.
├── manage.py
└── mysite
    ├── __init__.py
    ├── asgi.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

Con `manage.py` verificaremos si el proyecto de django funciona:

``` shell
python manage.py runserver
```

En el terminal tendremos probablemente la siguiente salida:

``` example
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).

You have 17 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.

November 28, 2022 - 12:12:11
Django version 3.0.5, using settings 'mysite.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```

Notar que tras la ejecución de `runserver` en nuestro proyecto han
aparecido carpetas llamadas `__pycache__` En nuestro archivo
`.gitignore` podemos excluirlas así como al entorno virtual:

``` example
venv/
__pycache__/
```

Finalmente también aparecen otros elementos en el proyecto como db.sqlite3:

``` example
.
├── db.sqlite3
├── manage.py
└── mysite
    ├── __init__.py
    ├── __pycache__/
    ├── asgi.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

## Analizar creación de proyecto

Si en la raíz de nuestro repositorio para la creación de nuestro
proyecto Django hubiesemos ejecutado lo siguiente:

``` shell
source venv/bin/activate
django-admin startproject mysite .
```

Notar hay un `.` tras mysite, ¿cambiaría la estructura?¿cómo podría
ejecutar el proyecto django ahora?

## Conectar a una base de datos

Para conectar a una base de datos, se debe modificar el archivo `settings.py` y agregar la siguiente configuración:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'django_init',
        'USER': 'root',
        'PASSWORD': 'root',
        'HOST': '127.0.0.1',
        'PORT': '3306',
    }
}
```

Note: Instalar el driver de MySQL para Python

```bash
pip install mysqlclient
```

### Ejecutar las migraciones

Para crear una base de datos, se debe ejecutar el siguiente comando:

```bash
python manage.py migrate
```

### Crear un super usuario

Para crear un super usuario, se debe ejecutar el siguiente comando y tener en cuenta que primero se debe crear la base de datos:

```bash
python manage.py createsuperuser
```

## Concepto de APP en Django

Una aplicación es un conjunto de modelos, vistas y controladores que se encargan de una funcionalidad específica. Por ejemplo, un proyecto de blog podría tener una aplicación para la gestión de usuarios, otra para la gestión de artículos y otra para la gestión de comentarios. Cada aplicación puede tener sus propios modelos, vistas y controladores.

En resumen un proyecto de Django puede tener muchas aplicaciones.

## Creación de una APP

Para crear una aplicación, se debe ejecutar el siguiente comando:

```bash
python manage.py startapp myapp
```

Luego de crear la aplicacion debemos agregarla a la lista de aplicaciones instaladas en el archivo `settings.py`:

```python
INSTALLED_APPS = [
    'myapp.apps.MyappConfig',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

Ahora la estructura del proyecto es la siguiente:

``` example
.
├── db.sqlite3
├── manage.py
├── myapp
│   ├── __init__.py
│   ├── __pycache__/
│   ├── admin.py
│   ├── apps.py
│   ├── migrations/
│   ├── models.py
│   ├── tests.py
│   └── views.py
└── mysite
    ├── __init__.py
    ├── __pycache__/
    ├── asgi.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

## Pasos para crear una nueva tabla

### Crear un modelo

Para crear un modelo, se debe crear un archivo llamado `models.py` en la carpeta `myapp` y agregar el siguiente código:

```python
from django.db import models

class Person(models.Model):
    name = models.CharField(max_length=100)
    description = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
```

Note: No hace falta colocar el `id` ya que Django lo crea por defecto.

### Crear las migraciones

Para crear las migraciones, se debe ejecutar el siguiente comando:

```bash
python manage.py makemigrations myapp
```

### Ejecutar las migraciones creadas

Para ejecutar las migraciones, se debe ejecutar el siguiente comando:

- Ejecuta las migraciones pendientes de myapp

```bash
python manage.py migrate myapp
```

- Ejecuta todas las migraciones pendientes de todas las apps del proyecto

```bash
python manage.py migrate 
```

*Revisar que la tabla se haya creado en la base de datos.*
