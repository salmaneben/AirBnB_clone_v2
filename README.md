# AirBnB Clone v2 🏠

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-2.0+-green.svg)](https://flask.palletsprojects.com/)
[![MySQL](https://img.shields.io/badge/MySQL-8.0+-orange.svg)](https://www.mysql.com/)
[![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-1.4+-red.svg)](https://www.sqlalchemy.org/)

A comprehensive clone of the AirBnB website, featuring both console-based management and web interface capabilities with dual storage engines (File and Database).

## 📋 Table of Contents

- [Features](#features)
- [Project Architecture](#project-architecture)
- [Installation](#installation)
- [Usage](#usage)
- [Storage Engines](#storage-engines)
- [Web Framework](#web-framework)
- [Deployment](#deployment)
- [Testing](#testing)
- [Project Structure](#project-structure)
- [Authors](#authors)

## ✨ Features

### Core Functionality
- **Object-Oriented Programming**: Well-structured models using inheritance
- **Dual Storage System**: File-based and MySQL database storage
- **Web Framework**: Flask-based web application with dynamic templates
- **RESTful API**: Complete CRUD operations via console and web interface
- **Data Persistence**: JSON serialization and MySQL database integration
- **Template Engine**: Jinja2 templates with responsive design
- **Deployment Ready**: Fabric scripts for automated deployment

### Models Implemented
- **BaseModel**: Parent class with common attributes and methods
- **User**: User management with authentication data
- **State**: Geographic state information
- **City**: City data linked to states
- **Place**: Accommodation listings with detailed information
- **Amenity**: Available amenities for places
- **Review**: User reviews for places

## 🏗️ Project Architecture

### Storage Engines
1. **FileStorage**: JSON-based file storage system
2. **DBStorage**: MySQL database with SQLAlchemy ORM

### Web Framework
- **Flask**: Lightweight WSGI web framework
- **Jinja2**: Template engine for dynamic HTML generation
- **Static Assets**: CSS styling and image resources

### Deployment Tools
- **Fabric**: Automated deployment scripts
- **Nginx**: Web server configuration
- **MySQL**: Production database setup

## 🚀 Installation

### Prerequisites
```bash
# Python 3.8+
sudo apt-get update
sudo apt-get install python3 python3-pip

# MySQL (for database storage)
sudo apt-get install mysql-server mysql-client

# Nginx (for web deployment)
sudo apt-get install nginx
```

### Setup Environment
```bash
# Clone the repository
git clone https://github.com/salmaneben/AirBnB_clone_v2.git
cd AirBnB_clone_v2

# Install Python dependencies
pip3 install flask
pip3 install sqlalchemy
pip3 install mysqlclient
pip3 install fabric

# Set up MySQL database (development)
cat setup_mysql_dev.sql | mysql -hlocalhost -uroot -p

# Set up MySQL database (testing)
cat setup_mysql_test.sql | mysql -hlocalhost -uroot -p
```

## 💻 Usage

### Console Interface

#### Starting the Console
```bash
# File storage mode (default)
./console.py

# Database storage mode
HBNB_MYSQL_USER=hbnb_dev HBNB_MYSQL_PWD=hbnb_dev_pwd HBNB_MYSQL_HOST=localhost HBNB_MYSQL_DB=hbnb_dev_db HBNB_TYPE_STORAGE=db ./console.py
```

#### Console Commands
| Command | Description | Example |
|---------|-------------|---------|
| `create` | Create new object | `create State name="California"` |
| `show` | Display object | `show State 1234-5678` |
| `all` | List all objects | `all State` |
| `update` | Modify object | `update State 1234-5678 name "Nevada"` |
| `destroy` | Delete object | `destroy State 1234-5678` |
| `count` | Count objects | `State.count()` |

#### Advanced Syntax Examples
```bash
# Create objects with parameters
(hbnb) create State name="California"
(hbnb) create City state_id="1234-5678" name="San Francisco"
(hbnb) create Place city_id="8765-4321" user_id="9999-8888" name="Lovely apartment" price_by_night=100 max_guest=4

# Alternative method syntax
(hbnb) User.all()
(hbnb) State.show("1234-5678")
(hbnb) Place.update("5555-4444", {"price_by_night": 150})
```

### Web Interface

#### Flask Development Server
```bash
# Basic Flask application
python3 -m web_flask.0-hello_route

# Full HBnB web application
HBNB_MYSQL_USER=hbnb_dev HBNB_MYSQL_PWD=hbnb_dev_pwd HBNB_MYSQL_HOST=localhost HBNB_MYSQL_DB=hbnb_dev_db HBNB_TYPE_STORAGE=db python3 -m web_flask.100-hbnb
```

#### Available Routes
| Route | Description |
|-------|-------------|
| `/` | Hello HBNB! |
| `/hbnb` | Main HBnB interface |
| `/states_list` | List all states |
| `/cities_by_states` | States with their cities |
| `/states/<id>` | Specific state information |
| `/hbnb_filters` | Search filters interface |

## 🗄️ Storage Engines

### File Storage
```python
# Environment variables for file storage (default)
export HBNB_TYPE_STORAGE=file
```
- Data stored in `file.json`
- JSON serialization/deserialization
- Suitable for development and testing

### Database Storage
```python
# Environment variables for database storage
export HBNB_TYPE_STORAGE=db
export HBNB_MYSQL_USER=hbnb_dev
export HBNB_MYSQL_PWD=hbnb_dev_pwd
export HBNB_MYSQL_HOST=localhost
export HBNB_MYSQL_DB=hbnb_dev_db
```
- MySQL database with SQLAlchemy ORM
- Relational data structure
- Production-ready with ACID compliance

## 🌐 Web Framework

### Static Web Pages
Located in `web_static/`:
- Progressive HTML/CSS development
- Responsive design elements
- Icon and image assets

### Dynamic Flask Application
Located in `web_flask/`:
- Route handling and URL mapping
- Template rendering with Jinja2
- Database integration for dynamic content

### Templates
Located in `web_flask/templates/`:
- Reusable HTML templates
- Dynamic content insertion
- Responsive layout design

## 🚀 Deployment

### Web Server Setup
```bash
# Set up web server for static content
sudo ./0-setup_web_static.sh
```

### Archive and Deploy
```bash
# Create deployment archive
python3 1-pack_web_static.py

# Deploy to servers
python3 2-do_deploy_web_static.py archive_path

# Full deployment pipeline
python3 3-deploy_web_static.py
```

### Cleanup
```bash
# Clean old deployments
python3 100-clean_web_static.py
```

## 🧪 Testing

### Running Tests
```bash
# Run all tests
python3 -m unittest discover tests

# Run specific test files
python3 -m unittest tests.test_models.test_base_model
python3 -m unittest tests.test_models.test_user

# Run with verbose output
python3 -m unittest discover tests -v
```

### Test Coverage
- **Unit Tests**: All model classes and storage engines
- **Integration Tests**: Console and web functionality
- **PEP8 Compliance**: Code style validation
## 📁 Project Structure

```
AirBnB_clone_v2/
├── 📁 models/                     # Data models and storage engines
│   ├── __init__.py               # Storage initialization
│   ├── base_model.py             # Base class for all models
│   ├── user.py                   # User model
│   ├── state.py                  # State model
│   ├── city.py                   # City model
│   ├── place.py                  # Place/accommodation model
│   ├── amenity.py                # Amenity model
│   ├── review.py                 # Review model
│   └── 📁 engine/                # Storage engines
│       ├── __init__.py
│       ├── file_storage.py       # JSON file storage
│       └── db_storage.py         # MySQL database storage
├── 📁 web_static/                # Static web content
│   ├── 📁 styles/                # CSS stylesheets
│   ├── 📁 images/                # Image assets
│   └── *.html                    # Static HTML pages
├── 📁 web_flask/                 # Flask web application
│   ├── 📁 templates/             # Jinja2 templates
│   └── *.py                      # Flask route handlers
├── 📁 tests/                     # Unit and integration tests
│   ├── 📁 test_models/           # Model tests
│   └── 📁 test_engine/           # Storage engine tests
├── console.py                    # Interactive command line interface
├── setup_mysql_dev.sql           # Development database setup
├── setup_mysql_test.sql          # Test database setup
├── *.py                          # Deployment and utility scripts
├── AUTHORS                       # Project contributors
└── README.md                     # This file
```

## 🔧 Environment Variables

### File Storage (Default)
```bash
export HBNB_TYPE_STORAGE=file
```

### Database Storage
```bash
export HBNB_TYPE_STORAGE=db
export HBNB_MYSQL_USER=hbnb_dev
export HBNB_MYSQL_PWD=hbnb_dev_pwd
export HBNB_MYSQL_HOST=localhost
export HBNB_MYSQL_DB=hbnb_dev_db
```

### Flask Configuration
```bash
export FLASK_APP=web_flask.app
export FLASK_ENV=development
```

## 📚 API Reference

### Console Commands

#### Object Creation
```bash
create <ClassName> [param1=value1] [param2=value2] ...
```

#### Object Retrieval
```bash
show <ClassName> <id>
<ClassName>.show(<id>)
```

#### Object Listing
```bash
all [ClassName]
<ClassName>.all()
```

#### Object Updates
```bash
update <ClassName> <id> <attribute> <value>
<ClassName>.update(<id>, <attribute>, <value>)
<ClassName>.update(<id>, {<dict>})
```

#### Object Deletion
```bash
destroy <ClassName> <id>
<ClassName>.destroy(<id>)
```

### Model Relationships

```
User (1) ──────── (*) Place ──────── (*) Review
                       │
                       │ (*) 
                       │
City (*) ──────── (1) State
 │
 │ (1)
 │
Place ──────────────── (*) Amenity
```

## 🎯 Key Features by Version

### v1 Features (Base Implementation)
- ✅ Object-oriented model design
- ✅ File-based storage system
- ✅ Interactive console interface
- ✅ Comprehensive unit testing

### v2 Features (Current)
- ✅ MySQL database integration
- ✅ Web framework with Flask
- ✅ Static and dynamic web content
- ✅ Deployment automation tools
- ✅ Template engine integration

### Future Features (v3+)
- 🔄 RESTful API endpoints
- 🔄 User authentication system
- 🔄 Advanced search functionality
- 🔄 Payment integration
- 🔄 Real-time notifications

## 🛠️ Development Guidelines

### Code Style
- **PEP8**: All Python code follows PEP8 standards
- **Documentation**: Comprehensive docstrings for all modules, classes, and methods
- **Type Hints**: Modern Python type annotations where applicable

### Testing Strategy
- **Unit Tests**: Individual component testing
- **Integration Tests**: End-to-end functionality testing  
- **Coverage**: Aim for 90%+ test coverage
- **Continuous Integration**: Automated testing pipeline

### Version Control
- **Git Flow**: Feature branch workflow
- **Commit Messages**: Conventional commit format
- **Code Review**: All changes require review before merge

## 🔍 Troubleshooting

### Common Issues

#### MySQL Connection Errors
```bash
# Check MySQL service
sudo systemctl status mysql

# Verify credentials
mysql -u hbnb_dev -p hbnb_dev_db
```

#### Permission Errors
```bash
# Fix file permissions
chmod +x console.py
chmod +x *.sh
```

#### Import Errors
```bash
# Add project root to Python path
export PYTHONPATH="${PYTHONPATH}:$(pwd)"
```

### Debug Mode
```bash
# Enable verbose console output
./console.py --debug

# Flask debug mode
export FLASK_DEBUG=1
```

## 📈 Performance Considerations

### Database Optimization
- **Indexing**: Strategic database indexing for frequently queried fields
- **Connection Pooling**: Efficient database connection management
- **Query Optimization**: Optimized SQLAlchemy queries

### Web Performance
- **Static Assets**: Efficient CSS and image serving
- **Template Caching**: Jinja2 template compilation caching
- **Response Compression**: Gzip compression for HTTP responses

## 🤝 Contributing

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/amazing-feature`)
3. **Commit** your changes (`git commit -m 'Add amazing feature'`)
4. **Push** to the branch (`git push origin feature/amazing-feature`)
5. **Open** a Pull Request

### Development Setup
```bash
# Clone your fork
git clone https://github.com/yourusername/AirBnB_clone_v2.git

# Set up virtual environment
python3 -m venv venv
source venv/bin/activate

# Install development dependencies
pip install -r requirements-dev.txt

# Run tests
python3 -m unittest discover tests
```

## 📄 License

This project is part of the ALX Software Engineering Program and is intended for educational purposes.

## 👥 Authors

- **Salmane Ben Yakhlaf** - *Lead Developer* 
- **El Mustapha Lakhloufi** - *Co-Developer*

See [AUTHORS](AUTHORS) for the complete list of contributors.

## 🙏 Acknowledgments

- **ALX Africa** - Software Engineering Program
- **Holberton School** - Educational methodology and project framework
- **AirBnB** - Inspiration for the project concept
- **Flask Community** - Web framework and documentation
- **SQLAlchemy Team** - ORM library and best practices

---

<div align="center">

**[⬆ Back to Top](#airbnb-clone-v2-)**

Made with ❤️ by the AirBnB Clone v2 Team

</div>
