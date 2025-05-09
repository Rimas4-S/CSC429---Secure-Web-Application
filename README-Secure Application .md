1-Project Overview (Insecure & Secure)
This project is a simple user management web application built with Flask.  
It demonstrates both insecure and secure coding practices to help identify and fix common web security vulnerabilities.  
The app allows users to register, login, post comments, and access dashboards.  
It highlights vulnerabilities SQL Injection, XSS, weak password storage, improper access control, and Lack of Encryption.

2-Steps to Run the Application:
To run our web application, we used Visual Studio Code on Windows. Inside our main project folder, we had two Python files: one for the insecure version (app_vulnerable.py) and one for the secure version (app.py). Each file runs separately and uses its own logic and security level, but both share the same structure and design.

We followed these steps to test the insecure version using Windows:

1-First, we opened the project folder in VS Code.

2-We created a virtual environment to isolate our project:
python -m venv venv

3-Then, we activated the environment:
venv\Scripts\activate

4-After that, we installed Flask:
pip install flask

5-For the vulnerable version, we ran:
python app_vulnerable.py

6-Finally, we opened the browser and visited:
http://127.0.0.1:5000 (e.g., vulnerable version )

In secure version, we followed these steps using using macOS:

1-Fisrt, we opened Terminal

2-Navigate to the project directory by running:
cd ~/Downloads/app2/app

3- Start the Flask server with HTTPS on port 5001 using your certificate and key:
flask run --port=5001 --cert=cert.pem --key=key.pem

4-Finally, we opened the browser and visited:
https://127.0.0.1:5001

The SSL certificate (cert.pem) used for running the Flask app has already been imported and trusted on the macOS system using Keychain Access. This ensures that the browser recognizes the certificate as valid when accessing the app over HTTPS (https://localhost:5001), without showing security warnings.

3-How to Test the Security Features
1.SQL Injection
- Go to the login page.
- Enter username: ' OR '1'='1' --
- Enter any password (e.g., 123)
- If it logs you in without a real account → SQL Injection vulnerability exists.

2.XSS
- After login, go to the dashboard.
- In the comment box, type:
  <script>alert('XSS')</script>
- If a popup appears when the page reloads → XSS is active.

3-Weak Password Storage
- Open vuln.db using DB Browser for SQLite.
- Go to "users" table.
- If you see plain passwords (like "123") → it's stored in plain text.

4-Access Control
- Directly visit: http://127.0.0.1:5000/admin
- If the page opens without asking for login or role check → no access control.

5-Encryption (in secure version only)
- Passwords are hashed using generate_password_hash().
- Session data is protected using Flask's secret_key.
- In secure version, HTTPS can be tested with SSL context.
- To test HTTPS locally, you must generate or use a self-signed SSL certificate (cert.pem, key.pem).

