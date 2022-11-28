# Django shell

Ejecutar a través del siguiente comando: (tener en cuenta la ubicación
desde donde lo invocaremos)

``` shell
python manage.py shell
```

Nos será de utilidad al tener modelos listos.

## Recordando

Tenemos la siguiente estructura del proyecto:

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

## Crear un registro desde la shell

Si ya hemos creado un modelo, podemos crear un registro desde la shell

*Estamos usando el modelo que creamos dentro de `myapp`*

- Crear un registro

```bash
from myapp.models import Person

person = Person(name='Juan', description='Estudiante')
person.save()
```

- Lista los registros

```bash
Person.objects.all()
```

- Obtener por un campo

```bash
Person.objects.get(pk=1)
Person.objects.get(name='Juan')
```

Nota: Recordar siempre importar el modelo que se desea utilizar.
