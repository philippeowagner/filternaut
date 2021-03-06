Filternaut
**********

Filternaut is a simple library which generates arbitrarily complex Django
Q-objects from simple data. It fits nicely into situations where users provide
data which you want to filter a queryset with.

Filternaut is indirectly a collection of fields, but it differs from Django
forms in that you specify the logical relationships between fields, as well
their names and types.

Filternaut is similar to Django Filters, but does not provide any machinery for
rendering a user interface and does not inspect your models to autogenerate
filters. However, Django Filters chains many calls to ``.filter()`` which means
OR-like behaviour with more than one join. Filternaut supports either
behaviour.

Quickstart
==========

.. code-block:: python

    # filters are combined using logical operators
    filters = (
        DateTimeFilter('created_date', lookups=['lt', 'gt']) &
        CharFilter('username', lookups=['icontains']))

    # they can read their values from anything dict-like
    filters.parse(request.GET)

    # and have a form-like 'validity pattern'.
    if filters.valid:
        queryset = queryset.filter(filters.Q)
    else:
        raise HttpResponseBadRequest(filters.errors)


Installation
============

.. code-block:: console

    $ pip install django-filternaut

Filternaut is compatible with:

- Python 2.7 and 3.4
- Django 1.2 through to 1.8 alpha 1
- Django REST Framework 2.4 and 3.0 (optional)

Documentation
=============

.. toctree::
   :hidden:

   self

.. toctree::
   :maxdepth: 2

   examples
   api
   tests
