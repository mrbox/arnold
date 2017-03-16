Creating Migrations
-------------------

Migrations are easy to setup. Simply create a `migration` folder
(with an `__init__.py`) and then start creating your migrations.

Migrations require two methods. `up` for creation and `down` for deletion.

Peewee has the ability to easily perform migrations such as adding a column. See `peewee docs <http://peewee.readthedocs.org/en/latest/peewee/playhouse.html#basic-schema-migrations>`_.

You must follow the naming convention `x_name` where `x` is a number, and `name` is a name for your personal reference. This will ensure that migrations are run in the correct order. Here is an example of some migration files: ::

  001_initial.py
  002_add_admin_to_users.py
  003_add_account_table.py

The basic template for a migration is as follows: ::

    def up:
      pass

    def down:
      pass

A more complete example of a migration file can be found `here <https://github.com/cam-stitt/arnold/blob/master/tests/arnold_config/migrations/001_initial.py>`_.

You can automatically create a migration file for migrations that create models. You want to do that to freeze state of models.
See following example, file 001_initial.py: ::

    db.create_table(SomeModel)

File 002_some_change.py: ::

    Add some_column to SomeModel

In this scenario if you run this migration against clean database, migration 002 will fail because migration 001 already created some_column.
To freeze models properly you can use `add_create_tables` method: ::

    $ arnold add_create_tables fully.qualified.path.SomeModel1 fully.qualified.path.SomeModel2 ...
