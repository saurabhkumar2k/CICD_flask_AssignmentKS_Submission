# CICD_flask_AssignmentKS
As per guideline for CI CD Pipeline, steps are followed as given below:
**Step 1**
ImageName: **CloneRepo**
<img width="1290" height="400" alt="image" src="https://github.com/user-attachments/assets/956b5e2f-076c-48a1-ba27-a674873a41e3" />

**Step 2**
We need to install the packages for dependencies of the project through command pip install -r requirements.txt
ImageName: **pipcommand**
<img width="1856" height="791" alt="image" src="https://github.com/user-attachments/assets/87a48613-e448-46a9-a4ce-679400f0664a" />

**Step 3**
Created new cluster in MongoDB Atlas and set the ConnectionString in .env file. Test the application with command "python app.py". And found it's working.
ImageName: **StudentRegistration**
<img width="1757" height="962" alt="image" src="https://github.com/user-attachments/assets/8c1d3515-ba4a-4369-9183-312f455d36b9" />

**AT THIS STAGE I HAVE ACHIEVED AS BELOW:**
a. **Flask application is in running state.**
b. **MongoDB Atlas connected sucessfully.**
c. **.env configured correctly.**
d. **Atlas authentication is working**

**Step 4**
As guided in documet, at least one health/status endpoint (e.g. /health) that the deployment step can use to confi rm the container actually started correctly on EC2. So app.py has been modified with code:
@app.route('/health')
def health():
    try:
        mongo.cx.admin.command('ping')
        return {
            "status": "UP",
            "database": "Connected"
        }, 200
    except Exception as e:
        return {
            "status": "DOWN",
            "error": str(e)
        }, 500
And tested the application and found its running.

**Step 5**
Install pytest explicitely as it was not installed
ImageName: **pytest**
<img width="1457" height="271" alt="image" src="https://github.com/user-attachments/assets/3726c75a-8d41-4de9-8aba-be83e15ff29c" />
ImageName: **Cnfpytest**
<img width="1412" height="257" alt="image" src="https://github.com/user-attachments/assets/e2f95632-20b1-465b-a13c-efe572e0f319" />
Run command python -m pytest -v and got the output 
ImageName: **CheckPytest**
<img width="1523" height="440" alt="image" src="https://github.com/user-attachments/assets/c929c7cf-0e2e-4748-af99-f4f9ca9ca9f5" />

**Step 6**
Created a file named **Dockerfile** in the project root:
Code for the file
FROM python:3.11-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["python", "app.py"]

**Step 7**
Created .dockerignore
.git
.github
__pycache__
*.pyc
.env
.pytest_cache
.vscode

**Step 8**
Started Docker Desktop
ImageName: **DockerDesktop**
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/678e9c50-1968-4d5b-bdde-059358f31a17" />



<img width="1502" height="540" alt="image" src="https://github.com/user-attachments/assets/574b697f-9ec7-4967-ae07-74c317f8e595" />



