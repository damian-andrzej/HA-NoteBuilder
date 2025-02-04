# Flask User Login App

## **Introduction**

This is a simple Flask app that allows users to register, log in, and view a protected dashboard. It uses Flask, Flask-SQLAlchemy for database management, and Flask-Bcrypt for password hashing.

---

## **Table of Contents**

- [Prerequisites](#prerequisites)
- [Setting Up the Project](#setting-up-the-project)
- [Creating the Database](#creating-the-database)
- [Running the App](#running-the-app)
- [Directory Structure](#directory-structure)
- [App Overview](#app-overview)
- [Additional Features You Can Add](#additional-features-you-can-add)
- [Contributing](#contributing)
- [License](#license)

---

## **Prerequisites**

Before getting started, ensure you have the following installed:

1. **Python 3.x**  
   Install from [Python.org](https://www.python.org/).

2. **pip** (Python Package Installer)  
   Install with Python or separately from [pip.pypa.io](https://pip.pypa.io/en/stable/).

3. **Git** (Optional but recommended)  
   Install from [Git SCM](https://git-scm.com/).

---

### **Setting Up the Project**

Follow these steps to set up your development environment:

## 1. **Clone the Repository**

Clone this repository to your local machine using Git:

```bash
git clone https://github.com/damian-andrzej/HA-NoteBuilder.git
cd HA-NoteBuilder

```
## 2. Create a Virtual Environment
Create a virtual environment to isolate the dependencies:

```bash
python -m venv venv
Activate the virtual environment:

Windows:
venv\Scripts\activate


Mac/Linux:
source venv/bin/activate
```

## 3. Install Required Dependencies
Install the dependencies listed in requirements.txt:

```bash
pip install -r requirements.txt
The required dependencies are:

Flask
Flask-SQLAlchemy
Flask-Bcrypt
```
## 4. Set Up Environment Variables (Optional)

Set up a .env file for your environment variables like SECRET_KEY for session handling. Here is an example of a env file:


SECRET_KEY=your_random_secret_key
Make sure to never commit your .env file to GitHub. Add it to your .gitignore:


echo ".env" >> .gitignore
Creating the Database
You need to create the database before running the app. Follow these steps:

# 1. Initialize the Database
Run the following Python script to create the database tables:

from app import db
db.create_all()
This will create the users.db file with the User model.

# 2. Manually Add a User (Optional)
If you want to manually add a user to the database, you can use the following code in the Python shell:

from app import db, bcrypt
from app import User

 Create a new user with a hashed password
hashed_password = bcrypt.generate_password_hash('password123').decode('utf-8')
user = User(username='admin', password=hashed_password)

 Add the user to the database
 
db.session.add(user)
db.session.commit()
Running the App


Once you have set up the database, you can run the Flask app:


1. Run the Flask App
Start the development server by running:
```
python app.py
```
2. Visit the App
Open your web browser and navigate to http://127.0.0.1:5000/ to view the app.

Visit the Login page at /login.
After logging in successfully, you will be redirected to the Dashboard page.


### **Directory Structure**
Here is a suggested directory structure for this Flask app:


flask-user-login-app/
│
├── app.py               # Main Flask application file
├── models.py            # Database models (User model)
├── config.py            # Configuration settings (e.g., database URI)
├── forms.py             # Form classes (if any, like registration)
├── templates/           # HTML templates
│   ├── login.html       # Login page template
│   ├── dashboard.html   # Dashboard page template
│   └── users.html       # List users page template
├── requirements.txt     # List of dependencies
├── .gitignore           # Git ignore file
└── .env                 # Environment variables (not committed to GitHub)


### **App Overview**
# 1. User Model:
The app uses an SQLAlchemy User model that has id, username, and password (hashed) fields.


class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(150), unique=True, nullable=False)
    password = db.Column(db.String(200), nullable=False)

    def __repr__(self):
        return f"User('{self.username}')"


## 2. Login Flow:
The app allows users to log in using a username and password. The password is securely hashed using Flask-Bcrypt and compared with the stored hash in the database.

## 3. Flask Routes:

/login: Displays the login form and processes user authentication.
/dashboard: Displays a protected page that can only be accessed by logged-in users.
## 4. Session Management:
The app uses Flask’s session object to keep track of the logged-in user.

## 5. Flash Messages:
Flash messages are used to give feedback to the user about login success or failure.

Additional Features - work in progress

User Registration: Implement a registration form where users can sign up by providing their username and password.
Password Reset: Implement a password reset feature where users can reset their forgotten password via email.
Rate Limiting: Implement rate-limiting to prevent brute force login attempts.

