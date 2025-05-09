1-Project Overview 

  This project is a simple user management web application built with Python Flask that demonstrates both vulnerable and secure coding practices. It allows users to register, log in, post comments, and access dashboards, with a special focus on five key web vulnerabilities:

  1- SQL Injection
  2- Cross-Site Scripting (XSS)
  3- Weak Password Storage
  4- Improper Access Control (RBAC)
  5- Lack of HTTPS Encryption

  By comparing the behavior of the insecure and secure versions side by side, this project helps illustrate how common web vulnerabilities can be exploited and how they can be prevented.

2- How to run Application
  2.1- Vlunerable version (app_vulnerable.py)
    Tested on Windows using VS Code
    - Open the project folder in VS Code.
    - Create a virtual environment:
    python -m venv venv
    - Activate the environment:
    venv\Scripts\activate
    - Install Flask:
    pip install flask
    - Run the insecure version:
    python app_vulnerable.py
    - Visit the application in your browser:
    http://127.0.0.1:5000

  2.2- Secure version (app.py)
    Tested on macOS with HTTPS
    - Open Terminal.
    - Navigate to the secure app directory:
    cd ~/Downloads/app2/app
    - Start the Flask server with HTTPS:
    flask run --port=5001 --cert=cert.pem --key=key.pem
    - Open your browser and go to:
    https://127.0.0.1:5001
    - Note:
      On macOS, the SSL certificate (cert.pem) has already been trusted using Keychain Access, so no browser security warnings appear.

3-How to Test the Security Features
  1.SQL Injection
  - Go to the login page.
  - Enter username: ' OR '1'='1' --
  - Enter any password (e.g., 123)
  - Vulnerable version: Logs you in even without a valid user.
  - Secure version: Login fails.

  2.XSS
  - After login, go to the dashboard.
  - In the comment box, type:
    <script>alert('XSS')</script>
  - Vulnerable version: A popup appears.
  - Secure version: Text is displayed as-is, no popup.

  3-Weak Password Storage
  - Open vuln.db using DB Browser for SQLite.
  - Go to "users" table.
  - Vulnerable version: Passwords are shown in plain text (like "123").
  - Secure version: Passwords are hashed.

  4-Access Control
  - Directly visit the admin panel: http://127.0.0.1:5000/admin
  - Vulnerable version: Page loads even if you're not an admin.
  - Secure version: Access is denied unless you're logged in as an admin.

  5-Encryption (in secure version only)
  - Run the secure version of the app using:
  flask run --port=5001 --cert=cert.pem --key=key.pem
  - Open your browser and go to:
  https://127.0.0.1:5001
  - Expected Results:
    - Vulnerable version: Runs over HTTP (http://127.0.0.1:5000), Data is transmitted in plaintext and can be intercepted.
    - Secure version: Runs over HTTPS → Communication is encrypted via SSL/TLS, protecting login credentials and session cookies.

  - Additional Details:
  Passwords are hashed using generate_password_hash() to ensure they are never stored in plaintext.
  Session data is secured using Flask’s secret_key.
  The SSL certificate (cert.pem) is imported and trusted locally (via Keychain Access on macOS), so no security warnings appear when accessing the app.

