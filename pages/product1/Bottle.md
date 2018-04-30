---
title: Bottle notes
tags: bottle, python
keywords: bottle
last_updated: April 30, 2018
summary: ""
sidebar: product1_sidebar
permalink: product1_bottle.html
---
# Overview
Bottle allows you to skip most of the html required to make a website with decorator functions(prefixed by @)
# Installation

~~~
pip install bottle
~~~

# Setup
~~~
import bottle
~~~
# GET Requests
## Route
~~~
@bottle.route('/login') #'actual location of the route' ie. http://localhost/8080/login
@bottle.route('register') #http://localhost/8080/register
~~~
Dynamic route
~~~
@bottle.route('/<id>') #Dynamic route
def article(id):
  return '<h1>You are viewing article' + id +'</h1>

@bottle.route('/page/<id>/<name>')
  def page(id,name):
    return '<h1>You are viewing article' + id +' with a anme of '+ name + '</h1>
~~~

## GET
~~~
@bottle.get('')
~~~
# POST Requests
## POST
~~~
@bottle.post('')
~~~

# VIEW Requests
## VIEW
~~~
@bottle.view('')
~~~

# Templates
Used to render the pages. Html & Python. saved as tpl files

~~~
template.py
@bottle.route('/')
def index():
  return bottle.template('index',  name='Benny')
~~~
### index.tpl
Python commands preceded by %
~~~
% if False:
  <h1>If Block</h1>
% else:
  <h1>Else Block </h1>
% end
~~~
Expressions closed by {{}}
~~~
% for i in range(10):
  <p> this is loop index: {{i}}</p>
% end
~~~
## Passing variables into the Templates
~~~
<h1> Hello {{ name }} </h1>
~~~

# Queries
~~~
@route('/querytest')
def querytest():
  param1 = bottle.request.query.param1
  return <h1>param1</h1>
# http://localhost/8080/querytest?param1=randominputvalue
~~~

### Returning Json data
~~~
...
  return {"name" : "jsondata", "mylist":[1,23,45,5]}
~~~

# Form Handling
For a form:
~~~
@bottle.route('/login')
def login():
    return '''
        <form action="/login" method="post">
            Username: <input name="username" type="text" />
            Password: <input name="password" type="password" />
            <input value="Login" type="submit" />
        </form>
~~~
Code to get the fields from the form
~~~
@bottle.route('/login', method='POST')
def do_login():
    username = bottle.request.forms.get('username')
    password = bottle.request.forms.get('password')
    if check_login(username, password):
        return "<p>Your login information was correct.</p>"
    else:
        return "<p>Login failed.</p>"
~~~
