=====
Emtex Common Utils
=====

This contains utility like permissions, audit log etc.

Detailed documentation is in the "docs" directory.

Quick start
-----------

1. Add "emtex_common_utils" to your INSTALLED_APPS setting like this::

    INSTALLED_APPS = [
        ...
        'emtex_common_utils',
    ]


Things available
-----------

1. Database Migrations::

    python manage.py emtex_migrate --for_date="YYYY-MM-DD"

