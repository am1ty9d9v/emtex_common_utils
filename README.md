# Emtex Common Utils

This contains utility like permissions, audit log etc.

Detailed documentation is in the "docs" directory.

## How to install

1. Using pip:
    
       pip install emtex_common_utils
    
    or add `emtex_common_utils` in your requirements.txt file and then run:
                
       pip install -r requirements.txt


## Quick start

1. Add "emtex_common_utils" to your INSTALLED_APPS setting like this:

       INSTALLED_APPS = [
            ...
            'emtex_common_utils',
       ]


## Things available

1. Database Migrations::

       python manage.py emtex_migrate --for_date="YYYY-MM-DD"

2. Logging:

       from emtex_common_utils.models import BaseModel, BaseLogModel
       from emtex_common_utils.mixins import BaseModelMixin

       ...

       class MyModelLog(BaseLogModel):
           """ Model to log changes for model MyModel """
           pass

       class MyModel(BaseModel, BaseModelMixin):
           """ Model which changes needs to be tracked. """

           class Meta:
               log_fields = (
                   my_field1, my_field2,
                   ...
               )
               log_model_name = MyModelLog
  
  
3. Handler functions inside `BaseModelMixin` that you can use to track changes:
* obj.has_changed(field_name)
* obj.get_old_value(field_name)
* obj.get_new_value(field_name)

P.S. `obj` here is the `MyModel` instance and `field_name` must be any field that is defined in `log_fields` in class `Meta` of model `MyModel`

4. Run raw SQL query using `sqlalchemy`.

       from emtex_common_utils.sqlalchemy_services import run_db_query
       sql_query = """
           select field_name1, field_name2 from some_database.some_model
               where some_field = 'some value'
       """
       results = run_db_query(sql_query)
