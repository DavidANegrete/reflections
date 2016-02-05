

# Flasking it up.

Here are the notes used to refine my understanding of the Flask framework. 

---
## Views
Views are created when they have routes. 
	
	@app.route('/')

---
## Passing and using Data 

To use the query string to pass data we must first import using the request 
object a value called ```args``` that hold all the arguments in the request 
to include POST and GET is used. 

	
	from flask import request
	

It is like a dictionary

#### Passing variables

Variables are then passed using the query string.
	
	
	def index(name="Your Name"):
	

#### Getting values from the request object
	
To get access to the args values in the abouve example. 

		
	name = request.args.get('name', name)
		
		
#### Passing values with a clean URL

Any variables passed named 'name' or just the standard index view is 
called below. A type can be indicated by appending the type 
using either: int, float or path, else it will be saved as a string.   

		
	@app.route('/')
	@app.route('/<name>')
		

Using @app.route('/<name>') iliminates the need to use 
		
			
	name = request.args.get('name', name)
			 

By adding an extra route to the view it either even can be passed or not
becuase it is implied in the route and if not passed the default value 
is passed. 

---
## Templates
	
To render a template with Flask we need a 'template' directory. Flask will look 
in the templates directory and render templates saved in that directory. 
	
	
	FlaskApp.py
		/templates
			example.html
	

To be able to render a template import render_template.

	
	from flask import render_template
	

To serve that template the return value must be render_template along with 
the name of the template getting rendered.

	
	return render_template("example.html")
	

#### Passing data to the view 
To get at the values and pass them to a template Flask uses Jinja2, it
uses {{ }} to access the variables when rendered.

	
	<p>Hello {{ name }}</p>
	

When the template is rendered the variable must be passed to get access to it.

	
	return render_template("example.html", name=name)
	

Or the variable can be passed as a dictionary.

	
	context = {'name' : name, 'age' : age}
	return render_template("example.html", **context)
	

#### Template Inheritance
Becuase you can inherit templates with Flask using inheritance helps to 
keep the code 'DRY'

To get acccess to a template from another template it has to be extended 
for example the base_layout.html template below acts as the container for
the blocks.

base_layout.html:

	<!doctype html>
		<head>
			<title>{% block title %}{% endblock %} </title>
		</head>
		<body>
			{% block content %}{% endblock %}
		</body>
	</html>


index.html:

	{% extends "base_layout.html" %}

	{% block title %}Hello!!{% endblock %}
	{% block content %}
	<p>Hello {{ name }}</p>
	{% endblock %}


Using the super class you can pass inherited content below a default title is passed.
	
base_layout.html:
	
	<!doctype html>
		<head>
			<title>{% block title %}Super Hello{% endblock %} </title>
		</head>
		<body>
			{% block content %}{% endblock %}
		</body>
	</html>


index.html:

	{% extends "base_layout.html" %}

	{% block title %}Hello!! | {{ super() }}{% endblock %}
	{% block content %}
	<p>Hello {{ name }}</p>
	{% endblock %}


--
## Forms
Just like you create views you for pages you do the same when posting templates
information.  

	@app.route('/save', methods=[POST])
	def save():
		return 'Saved!'

In the template the action taken has to be requested using 'url_for'.

	<form action="{{ url_for('save') }}">
		<input>...</input>
	</form>

To use url_for it has to be imported.

	from flask import url_for

To redirect after the form is submitted import redirect.

	from flask import redirect

Rending and redirecting if the index file had a POST request.  

	@app.route('/save', methods=[POST])
	def save():
		return redirect(url_for('index.html')

## Cookies
They are used to store data between requests they are set on the response, unlike 
other framework like Django or JS. 

Responses are not created until the the return is executed so make_response is imported
to do just that. 


	from flask import make_response
 

Wihin a called method you can return a response like so:

	def save():
		response = make_response(redirect(url_for('index.html')))
		# bc request.form is an immutable dict
				response.set_cookie('whatever', json.dumps(dict(request.form.items()))


Now say you want to save form information into jason. you could do it like so.
	
	...
	def get_saved_data():
		try:
			# turning data into Python code once more
			data = json.loads(request.cookies.get('whatever'))
		except TypeError:
			data = {}
		return data

To save that data.

	def save():
		response = make_response(redirect(url_for('index.html')))

		data = get_saved_data()
		data.update(dict(request.form.itmes()))
		response.set_cookie('whatever', json.dumps(dict(data))
		return response
