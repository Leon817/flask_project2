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

## Getting stuff to work: Tables

Looking at **database_app.py** lines 26–45, you can see how you explain a table to [Flask-SQLAlchemy](http://flask-sqlalchemy.pocoo.org/). The name of the table in my database is **socks** and the convention is to uppercase the class name (**Sock**) and also make it singular in creating the class.

```
class Sock(db.Model):
    __tablename__ = 'socks'
```

You can set up your table or tables as you see here. If you have questions about the datatypes (String, etc.) see the [SQLAlchemy docs](http://docs.sqlalchemy.org/en/latest/core/type_basics.html).

## Getting stuff to work: Routes

There is only one route in this app (see **database_app.py**), and it demonstrates two ways to get data out of your database.

```
@app.route('/')
def index():
    socks = Sock.query.all()
    foo = Sock.query.filter_by(id='16').first()
    return render_template('index.html', socks=socks, foo=foo)
```

The variable **socks** in this route is going to contain every row in the table, which makes it good for looping. You'll see that in the template in a sec.

The variable **foo** in this route contains only the data from one row -- the row with the unique ID "16."

Note how we must include the two variables explicitly in `render_template()` at the end of the route function.

## How the template uses the data

Open **templates/index.html** to see how the two variables from the route can be used. You can find **socks** and **foo** in the code in lines 13 and 18. Dot-syntax is used to access the individual columns (db fields) in the row (db record).

A for-loop in [Jinja2](http://jinja.pocoo.org/docs/dev/) syntax is used to loop through every record contained in **socks** and show the name and color for each.

The desired fields from the **foo** record (row) are just dropped in among normal punctuation and HTML tags.
