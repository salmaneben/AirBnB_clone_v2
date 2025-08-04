# Web Flask 🌐

A Flask-based web application that serves dynamic content for the AirBnB clone project, featuring template rendering, database integration, and RESTful route handling.

## 📋 Overview

The web_flask directory contains a progressive series of Flask applications that demonstrate web development concepts from basic routing to full-featured web applications with database integration and dynamic template rendering.

## 🗂️ Directory Structure

```
web_flask/
├── 📁 templates/                 # Jinja2 templates
│   ├── 5-number.html           # Number display template
│   ├── 6-number_odd_or_even.html # Odd/even number template
│   ├── 7-states_list.html      # States listing template
│   ├── 8-cities_by_states.html # Cities by states template
│   ├── 9-states.html           # State details template
│   ├── 10-hbnb_filters.html    # Search filters template
│   └── 100-hbnb.html           # Full HBnB application template
├── 📁 __pycache__/              # Python bytecode cache
├── 0-hello_route.py             # Basic Flask route
├── 1-hbnb_route.py              # Multiple routes
├── 2-c_route.py                 # Variable routes
├── 3-python_route.py            # Default parameters
├── 4-number_route.py            # Type conversion
├── 5-number_template.py         # Template rendering
├── 6-number_odd_or_even.py      # Conditional templates
├── 7-states_list.py             # Database integration
├── 8-cities_by_states.py        # Related data display
├── 9-states.py                  # Dynamic state details
├── 10-hbnb_filters.py           # Search interface
├── 100-hbnb.py                  # Complete web application
└── README.md                    # This file
```

## 🎯 Development Progression

### Phase 1: Basic Routing (0-4)
Learn fundamental Flask concepts and URL routing

### Phase 2: Template Integration (5-6)
Master Jinja2 template engine and dynamic content

### Phase 3: Database Integration (7-9)
Connect Flask to storage engines and display data

### Phase 4: Complete Application (10-100)
Build full-featured web application with filters and search

## 🚀 Getting Started

### Prerequisites
```bash
# Install Flask
pip3 install Flask

# Install SQLAlchemy (for database integration)
pip3 install SQLAlchemy mysqlclient

# Set up environment variables
export PYTHONPATH="$PWD:$PYTHONPATH"
```

### Running Applications
```bash
# Basic applications (0-6)
python3 -m web_flask.0-hello_route
python3 -m web_flask.1-hbnb_route
python3 -m web_flask.2-c_route

# Database-integrated applications (7-100)
HBNB_MYSQL_USER=hbnb_dev HBNB_MYSQL_PWD=hbnb_dev_pwd HBNB_MYSQL_HOST=localhost HBNB_MYSQL_DB=hbnb_dev_db HBNB_TYPE_STORAGE=db python3 -m web_flask.100-hbnb
```

## 📋 Application Details

### 0-hello_route.py
**Basic Flask Application**
```python
# Simple route demonstration
@app.route("/airbnb-onepage/", strict_slashes=False)
def hello_hbnb():
    return "Hello HBNB!"
```
- **Purpose**: Introduction to Flask and basic routing
- **Routes**: `/airbnb-onepage/`
- **Features**: Simple text response

### 1-hbnb_route.py
**Multiple Routes**
```python
# Multiple route handling
@app.route("/", strict_slashes=False)
@app.route("/hbnb", strict_slashes=False)
```
- **Purpose**: Multiple route definitions
- **Routes**: `/`, `/hbnb`
- **Features**: Route flexibility with strict_slashes

### 2-c_route.py
**Variable Routes**
```python
# URL variables and text processing
@app.route("/c/<text>", strict_slashes=False)
def c(text):
    return "C {}".format(text.replace("_", " "))
```
- **Purpose**: URL variable handling
- **Routes**: `/`, `/hbnb`, `/c/<text>`
- **Features**: Text manipulation and variable routes

### 3-python_route.py
**Default Parameters**
```python
# Optional parameters with defaults
@app.route("/python", strict_slashes=False)
@app.route("/python/<text>", strict_slashes=False)
def python(text="is cool"):
    return "Python {}".format(text.replace("_", " "))
```
- **Purpose**: Optional URL parameters
- **Routes**: Previous routes + `/python/(<text>)`
- **Features**: Default parameter values

### 4-number_route.py
**Type Conversion**
```python
# Integer type conversion
@app.route("/number/<int:n>", strict_slashes=False)
def number(n):
    return "{} is a number".format(n)
```
- **Purpose**: URL type conversion and validation
- **Routes**: Previous routes + `/number/<int:n>`
- **Features**: Integer validation and conversion

### 5-number_template.py
**Template Rendering**
```python
# Jinja2 template integration
@app.route("/number_template/<int:n>", strict_slashes=False)
def number_template(n):
    return render_template("5-number.html", n=n)
```
- **Purpose**: Template engine integration
- **Routes**: Previous routes + `/number_template/<int:n>`
- **Features**: Jinja2 template rendering with variables

### 6-number_odd_or_even.py
**Conditional Templates**
```python
# Template logic and conditionals
@app.route("/number_odd_or_even/<int:n>", strict_slashes=False)
def number_odd_or_even(n):
    return render_template("6-number_odd_or_even.html", n=n)
```
- **Purpose**: Template conditionals and logic
- **Routes**: Previous routes + `/number_odd_or_even/<int:n>`
- **Features**: Template conditional rendering

### 7-states_list.py
**Database Integration**
```python
# Storage engine integration
from models import storage

@app.route("/states_list", strict_slashes=False)
def states_list():
    states = storage.all("State")
    return render_template("7-states_list.html", states=states)
```
- **Purpose**: Database connection and data display
- **Routes**: `/states_list`
- **Features**: Storage engine integration, data sorting

### 8-cities_by_states.py
**Related Data Display**
```python
# Relationship data handling
@app.route("/cities_by_states", strict_slashes=False)
def cities_by_states():
    states = storage.all("State")
    return render_template("8-cities_by_states.html", states=states)
```
- **Purpose**: Related model data display
- **Routes**: `/cities_by_states`
- **Features**: State-city relationships, nested data

### 9-states.py
**Dynamic State Details**
```python
# Dynamic content based on URL parameters
@app.route("/states/<id>", strict_slashes=False)
def states_id(id):
    for state in storage.all("State").values():
        if state.id == id:
            return render_template("9-states.html", state=state)
    return render_template("9-states.html")
```
- **Purpose**: Dynamic content based on parameters
- **Routes**: `/states`, `/states/<id>`
- **Features**: Conditional content, error handling

### 10-hbnb_filters.py
**Search Interface**
```python
# Search filters integration
@app.route("/hbnb_filters", strict_slashes=False)
def hbnb_filters():
    states = storage.all("State")
    amenities = storage.all("Amenity")
    return render_template("10-hbnb_filters.html",
                         states=states, amenities=amenities)
```
- **Purpose**: Search and filter interface
- **Routes**: `/hbnb_filters`
- **Features**: Multiple model integration, search UI

### 100-hbnb.py
**Complete Web Application**
```python
# Full-featured HBnB application
@app.route("/hbnb", strict_slashes=False)
def hbnb():
    states = storage.all("State")
    amenities = storage.all("Amenity")
    places = storage.all("Place")
    return render_template("100-hbnb.html",
                         states=states, amenities=amenities, places=places)
```
- **Purpose**: Complete web application
- **Routes**: `/hbnb`
- **Features**: Full data integration, complete UI

## 🎨 Template Features

### Jinja2 Integration
```html
<!-- Variable rendering -->
<h1>Number: {{ n }}</h1>

<!-- Conditional logic -->
{% if n % 2 == 0 %}
    <p>{{ n }} is even</p>
{% else %}
    <p>{{ n }} is odd</p>
{% endif %}

<!-- Loop iteration -->
{% for state in states.values()|sort(attribute="name") %}
    <li>{{ state.name }}</li>
{% endfor %}
```

### Template Inheritance
```html
<!-- Base template structure -->
<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}{% endblock %}</title>
</head>
<body>
    {% block content %}{% endblock %}
</body>
</html>
```

### Filter Usage
```html
<!-- Jinja2 filters for data manipulation -->
{{ states.values()|sort(attribute="name") }}
{{ place.price_by_night|int }}
{{ review.text|safe }}
```

## 🔧 Configuration

### Environment Variables
```bash
# Database storage configuration
export HBNB_TYPE_STORAGE=db
export HBNB_MYSQL_USER=hbnb_dev
export HBNB_MYSQL_PWD=hbnb_dev_pwd
export HBNB_MYSQL_HOST=localhost
export HBNB_MYSQL_DB=hbnb_dev_db

# Flask configuration
export FLASK_APP=web_flask.app
export FLASK_ENV=development
export FLASK_DEBUG=1
```

### Application Configuration
```python
# Flask app configuration
app = Flask(__name__)
app.jinja_env.trim_blocks = True
app.jinja_env.lstrip_blocks = True

# Template auto-reloading
app.config['TEMPLATES_AUTO_RELOAD'] = True
```

## 🎯 Key Features

### URL Routing
- **Static routes**: Fixed URL patterns
- **Variable routes**: Dynamic URL parameters
- **Type conversion**: Automatic parameter validation
- **Optional parameters**: Default values support

### Template Engine
- **Jinja2 integration**: Powerful template syntax
- **Variable injection**: Dynamic content rendering
- **Control structures**: Loops and conditionals
- **Filter system**: Data transformation

### Database Integration
- **Storage abstraction**: Unified data access
- **Model relationships**: Foreign key handling
- **Data sorting**: Template-level sorting
- **Error handling**: Graceful failure management

### Response Handling
- **Content negotiation**: Appropriate response types
- **Error pages**: Custom error handling
- **Teardown handlers**: Resource cleanup
- **Session management**: Request lifecycle

## 🛠️ Development Tools

### Debugging
```python
# Enable debug mode
if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000, debug=True)
```

### Testing Routes
```bash
# Test individual routes
curl http://localhost:5000/
curl http://localhost:5000/states_list
curl http://localhost:5000/number/89
```

### Template Development
```bash
# Auto-reload templates
export FLASK_ENV=development
export FLASK_DEBUG=1
```

## 🔍 Troubleshooting

### Common Issues

#### Import Errors
```bash
# Fix Python path
export PYTHONPATH="${PYTHONPATH}:$(pwd)"
```

#### Database Connection
```bash
# Verify database credentials
mysql -u hbnb_dev -p hbnb_dev_db
```

#### Template Not Found
```bash
# Check template directory structure
ls -la web_flask/templates/
```

#### Port Already in Use
```bash
# Find and kill process
lsof -ti:5000 | xargs kill -9
```

## 📈 Performance Optimization

### Template Caching
```python
# Enable template caching
app.jinja_env.cache_size = 1000
```

### Static Files
```python
# Static file serving
app.static_folder = 'static'
app.static_url_path = '/static'
```

### Database Optimization
```python
# Connection pooling
@app.teardown_appcontext
def teardown(exc):
    storage.close()
```

## 🚀 Deployment

### Production Configuration
```python
# Production settings
app.config['DEBUG'] = False
app.config['TESTING'] = False
```

### WSGI Integration
```python
# WSGI application
from web_flask.100-hbnb import app

if __name__ == "__main__":
    app.run()
```

### Nginx Configuration
```nginx
# Proxy Flask application
location / {
    proxy_pass http://127.0.0.1:5000;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
}
```

## 🤝 Contributing

### Adding New Routes
1. **Create new Python file**: Follow naming convention
2. **Define routes**: Use consistent patterns
3. **Add templates**: Create corresponding HTML files
4. **Test functionality**: Verify all routes work
5. **Update documentation**: Add to this README

### Best Practices
- **Route organization**: Group related routes
- **Error handling**: Implement proper error responses
- **Template structure**: Use consistent HTML structure
- **Documentation**: Comment complex logic

---

<div align="center">

**Part of the AirBnB Clone v2 Project**

Demonstrating Flask web development from basics to production

</div>
