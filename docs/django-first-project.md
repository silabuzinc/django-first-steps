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

1.  Desde la shell de Python
2.  Directamente desde el terminal
3.  A través de pip freeze

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

# Inicializando repositorio (opcional)

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

# Creación de primer projecto Django

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

# Analizar creación de proyecto

Si en la raíz de nuestro repositorio para la creación de nuestro
proyecto Django hubiesemos ejecutado lo siguiente:

``` shell
source venv/bin/activate
django-admin startproject mysite .
```

Notar hay un `.` tras mysite, ¿cambiaría la estructura?¿cómo podría
ejecutar el proyecto django ahora?