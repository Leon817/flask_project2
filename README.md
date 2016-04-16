# Basic Flask app with a MySQL database

This app only reads from an existing database. It does not write to the database or update it.

There are two versions of the app:

* database_app.py - Runs locally and accesses a MySQL/MariaDB database (with only one table) that is running in [XAMPP](https://www.apachefriends.org/index.html) on a Mac.
* socks.py - Exactly the same app, accessing the same database, but with modifications so it works on [PythonAnywhere](https://www.pythonanywhere.com/).

Another file is not part of the app at all, but was useful for testing the database connection on both systems:

* local_db_setup.py

Finally, the templates:

* base.html - The Bootstrap base file from [Flask-Bootstrap](https://pythonhosted.org/Flask-Bootstrap/).
* index.html - The one template that opens in this app. Open this file to see the dynamic stuff and how it is formatted.
* 404.html - Template for the 404 error page.
* 500.html - Template for the 500 error page.
