# Automagic REST

Automagic REST automatically builds a full Django app as a Django REST Framework read-only environment for a set of tables in a PostgreSQL database.

This is very much in heavy development, being extracted from a production system and genericized for open source release.

## Installation

To get started, `pip install automagic-rest` and add `automagic_rest` to your `INSTALLED_APPS` setting in Django.

## Configuration and Customization

By default, Automagic REST will create a directory called `data` at the root of your Django project, where `manage.py` lives.

Methods are provided which can be overridden to customize the endpoint.

#### class automagic_rest.management.commands.build_data_models.Command

`get_db` (default: `my_pg_data`): the name of the PostgreSQL database in Django's settings that we will introspect to build the API.

`get_owner` (default: `my_pg_user`): the name of the PostgreSQL user that owns the schemata we will introspect.

`get_allowed_schemata` (default: `None`): if set, returns a list of schemata in the database to be built. If `None`, selects all schemata for the specific user.

`get_root_python_path` (default: `data_path`): a Python path where you would like to write the models, serializers, and routes. **IMPORTANT**: this path will be wiped and re-written every time the build command is run. It should be a dedicated directory with nothing else in it.

`get_serializer` (default: `rest_framework.serializers.ModelSerializer`): the serializer to use.

`get_view` (default: `automagic_rest.views.GenericViewSet`): the view to use.

`get_router` (default: `rest_framework.routers.DefaultRouter`): the router to use.

`sanitize_sql_identifier`: this method takes a string, and sanitizes it for injections into SQL, allowing only alphanumerics and underscores.

`metadata_sql`: this method returns the SQL used to pull the metadata from PostgreSQL to build the endpoints.


