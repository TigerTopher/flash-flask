# flash-flask: get started with flask

```
date = "2015-02-10T02:11:02+08:00"
title = "Learn Flask"
authors = ["toph", "carl"]
```

In this guide, we’ll cover installing Flask and using it for the first time. Flask is a back-end framework that we will be using alongside HTML and CSS. Contrary to to the front end, which is basically what the client sees, the back end consists of the internal mechanisms of a website, which handles stuff like input from the client.

After completing this tutorial, you will be able to:
* Set-up Flask in your machines
* Number 2
* Implement CRUD operations in Flask

This guide is based directly from the awesome and concise guides provided by [Flask Documentation](http://flask.pocoo.org/docs/0.10/) and [Miguel Grinberg](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world). These guides have been merged and modified for UP CSI Devcamp 2015.

```
Guide Outline:
Foreword
I. Installing Flask
  A. Linux Guide
  B. Windows Guide  
II. Hello World in Flask
```

## Foreword: Why Flask?
Why flask? Why study a microframework if I could just study real `frameworks` such as Django? Why should I waste my time learning Flask?

A short, simple answer is that many developers use frameworks such as RoR and Django to develop sites whose functionalities doesn't really need to use such sophisticated, complicated frameworks. Why not simplify things o'rayt? Also, the learning curve for complete frameworks are way-way steeper than microframeworks. Surely, Flask is a suitable stepping stone for first-time non-framework developers.

Please read this 2-minute article before starting with Flask. [Check out this link.](http://flask.pocoo.org/docs/0.10/foreword/#what-does-micro-mean):


## I. Installing Flask

To install Flask, we would be needing to 3 things:
1. Python 3 - a widely used general-purpose, high-level programming language.

2. pip - a tool that's used to manage packages written in Python

3. Virtual Environment (Virtualenv)- allows us to create Python environments that are isolated from one another. We will now create our own virtual environment for a simple web app and install Flask in it.

To learn more about one of the best programming language, check out [Python's Website](https://www.python.org/).

For a  thorough beginner-level explanation for pip and Virtualenv, you could check out this awesome [article](http://www.dabapps.com/blog/introduction-to-pip-and-virtualenv-python/).

For Unix-based Operating Systems
---
On Ubuntu, Linux Mint, or other distributions that have `apt-get`, run the command:
```
sudo apt-get install python3.4-venv
```
This will allow us to create Python environments that are isolated from one another.

Type these on the command line in order to make the virtual environment:
```
mkdir microblog
cd microblog
python3 -m venv flask
```
(note: the name microblog can be substituted with anything)

To install Flask and other stuff, copy this to the command line:
```
flask/bin/pip install flask
flask/bin/pip install flask-login
flask/bin/pip install flask-openid
flask/bin/pip install flask-mail
flask/bin/pip install flask-sqlalchemy
flask/bin/pip install sqlalchemy-migrate
flask/bin/pip install flask-whooshalchemy
flask/bin/pip install flask-wtf
flask/bin/pip install flask-babel
flask/bin/pip install guess_language
flask/bin/pip install flipflop
flask/bin/pip install coverage
```

And we're done! Let's proceed to our First Web App in Flask!

For Windows
===
One main difference between Windows from Unix-based OS is that you need to edit your system environment variables in order to run python in the command prompt.

Luckily, both the (1) system environment variables can already be updated and (2) pip can already be installed during the Python 3.4 installation. In order to accomplish that, you can do the following:

1.) Quick-Guide: Python 3.4 Installation
    For a thorough guide, you can click this [link](google.com).

  a. Download python 3.4 [here](https://www.python.org/downloads/).

  b. Run (as administator) the downloaded exe file.

  c. Select `Customize Installation`

  d. In Optional Feature, tick the checkbox `pip`. Click `next`.

  e. In Advanced Options, tick the checkbox `Add Python to environment variables`. Click `Install`

2.) Pip Installation

  If you did Step 1, then you don't need to do this.

  Else if you have installed Python before but didn't decide to install pip, then do the following:

  Enter the following in our command line:
```
python -m easy_install pip
```
  The command above makes use of easy_install, a primitive package manager (same as pip) that is installed automatically when you install python.

3.) Installing Virtualenv

  In your command line, enter:
```
python -m pip install virtualenv
```

4.) Setup application folder

  Type these on the command line in order to make the virtual environment:
```
mkdir microblog
cd microblog
virtualenv venv
```
  (note: the name microblog can be substituted with anything)

  Now, whenever you want to work on a project, you only have to activate the corresponding environment.
```
$ venv\scripts\activate
```
  Either way, you should now be using your virtualenv (notice how the prompt of your shell has changed to show the active environment).
  Now you can just enter the following command to get Flask activated in your virtualenv:
```
$ pip install Flask
```

Next, do this...
```
$ venv\Scripts\pip install flask-login
$ venv\Scripts\pip install flask-openid
$ venv\Scripts\pip install flask-mail
$ venv\Scripts\pip install flask-sqlalchemy
$ venv\Scripts\pip install sqlalchemy-migrate
$ venv\Scripts\pip install flask-whooshalchemy
$ venv\Scripts\pip install flask-wtf
$ venv\Scripts\pip install flask-babel
$ venv\Scripts\pip install guess_language
$ venv\Scripts\pip install flipflop
$ venv\Scripts\pip install coverage
```

These commands will download and install all the packages that we will use for our application.

And we're done! Let's proceed to our First Web App in Flask!

## II. "Hello World" in Flask!

We now have a venv sub-folder inside your microblog folder that is populated with a Python interpreter and the Flask framework and extensions that we will use for this application.

`cd` to the `microblog` folder. We will create the basic folder structure for our application:

```
$ mkdir app
$ mkdir app/static
$ mkdir app/templates
$ mkdir tmp
```

**WHAT ARE THESE FOLDERS**

The `app` folder will be where we will put our application package.
The `static` sub-folder is where we will store static files like images, javascripts, and cascading style sheets.
The `templates` sub-folder is obviously where our templates will go.

Let's start by creating a simple init script for our `app` package (`file app/__init__.py`):

```
from flask import Flask

app = Flask(__name__)
from app import views
```

The script above simply creates the application object (of class Flask) and then imports the `views` module, which we haven't written yet. Do not confuse `app` the variable (which gets assigned the `Flask` instance) with `app` the package (from which we import the `views` module).

If you are wondering why the import statement is at the end and not at the beginning of the script as it is always done, the reason is to avoid circular references, because you are going to see that the views module needs to import the app variable defined in this script. Putting the import at the end avoids the circular import error.

**WHAT ARE VIEWS?**

The views are the handlers that respond to requests from web browsers or other clients. In Flask handlers are written as Python functions. Each view function is mapped to one or more request URLs.

Now let's write our first view function (file `app/views.py`):

```
from app import app

@app.route('/')
@app.route('/index')
def index():
    return "Hello, World!"
```

This `view` is actually pretty simple, it just returns a string, to be displayed on the client's web browser. The two `route` decorators above the function create the mappings from URLs `/` and `/index` to this function.

You might want to check out this [site to learn more about Python Decorators](https://realpython.com/blog/python/primer-on-python-decorators/)

The final step to have a fully working web application is to create a script that starts up the development web server with our application. Let's call this script `run.py`, and put it in the root folder:

```
#!flask/bin/python
from app import app
app.run(debug=True)
```

The script simply imports the app variable from our app package and invokes its run method to start the server. Remember that the app variable holds the Flask instance that we created it above.

Before we start the app, let's verify if our directory is correct. It must look like this (except instead of my_app it would be microblog):

![Directory Image](https://fbcdn-sphotos-c-a.akamaihd.net/hphotos-ak-xlf1/v/t34.0-12/12177706_1213462125337486_431659876_n.jpg?oh=b28483a4a964e826dd2043a24ae9ccec&oe=562F6F82&__gda__=1446031431_1b570c98a7ae22341ffe082c80def9c0)

**Starting the App**

To start the app you just run this script. On OS X, Linux and Cygwin you have to indicate that this is an executable file before you can run it:

```
$ chmod a+x run.py
```


Then the script can simply be executed as follows:
```
./run.py
```

On Windows the process is a bit different. There is no need to indicate the file is executable. Instead you have to run the script as an argument to the Python interpreter from the virtual environment:

```
$ venv\Scripts\python run.py
```

After the server initializes it will listen on port 5000 waiting for connections. Now open up your web browser and enter the following URL in the address field:

```
http://localhost:5000
```

Alternatively you can use the following URL:

```
http://localhost:5000/index
```

Do you see the route mappings in action? The first URL maps to /, while the second maps to /index. Both routes are associated with our view function, so they produce the same result. If you enter any other URL you will get an error, since only these two have been defined.

When you are done playing with the server you can just hit Ctrl-C to stop it.

## III. Templates

We have made our webApp running. Now let's try to expand it!

Let's try to combine what we've learned in our previous DevCamp session/s: HTML and Python.

Copy the following in your `views.py` file:
```

from app import app

@app.route('/')
@app.route('/index')
def index():
    user = {'nickname': 'Toph'}
    return '''
<html>
    <head>
        <title>Home Page</title>
    </head>
    <body>
        <h1>Hello, ''' + user['nickname'] + '''! Why you so pogi?<h1>
    </body>
</html
'''

```

You should see something like this:
![SomethinLikeThis](https://scontent-hkg3-1.xx.fbcdn.net/hphotos-xpa1/v/t34.0-12/12179844_1214551965228502_1186999711_n.jpg?oh=1a8ea1c91c74a332edd886450dce86da&oe=56331D34)

So what happened?






## References
All thanks to Miguel Grinberg's [Mega-Tutorial Site](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).
