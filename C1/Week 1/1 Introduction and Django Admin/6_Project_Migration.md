# Project Migration

The final piece of set up is to run the database migrations with the `migrate` management command in the terminal.

```bash
python3 manage.py migrate
```

If successful, you should see the following output:

```bash
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying admin.0003_logentry_add_action_flag_choices... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying auth.0009_alter_user_last_name_max_length... OK
  Applying auth.0010_alter_group_name_max_length... OK
  Applying auth.0011_update_proxy_permissions... OK
  Applying auth.0012_alter_user_first_name_max_length... OK
  Applying sessions.0001_initial... OK
```

A user needs to be created, to be able to log into the Django admin site. This is done in the terminal with the `createuser` management command.

```bash
python3 manage.py createsuperuser
```

If successful, you should see the following interaction. You can use your own username, email, and password. Be sure to remember them as this information will be used throughout this project.

```bash
Username (leave blank to use 'codio'):
Email address: codio@example.com
Password: password
Password (again): password
This password is too common.
Bypass password validation and create user anyway? [y/N]: y
Superuser created successfully.
```

Note that you see the warning *This password is too common.* , because I’ve decided to literally use the password *password* here. This is fine if you’re the only person using the application for testing, but definitely not recommended for production!

## Reading Question

When do you need to be doing migrations in Django?

- You have to run a migration every time you want to start your Django dev server.
- ***You need to run a migration when you want the changes made to your models to be stored in a database.***
- You only have to run a migration when first starting your Django project. After that, you never have to do it again.

The correct answer is:

```markdown
You need to run a migration when you want the changes made to your models to be stored in a database.
```

Migrations are only needed when changes are made to models.
