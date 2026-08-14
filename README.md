# CICD_flask_AssignmentKS
As per guideline for CI CD Pipeline, steps are followed as given below:
**Step 1**
ImageName: **CloneRepo**
<img width="1290" height="400" alt="image" src="https://github.com/user-attachments/assets/db00c717-bbff-4064-a603-59a5a3970d40" />

**Step 2**
We need to install the packages for dependencies of the project through command pip install -r requirements.txt
ImageName: **pipcommand**
<img width="1856" height="791" alt="image" src="https://github.com/user-attachments/assets/20b5da9f-51c9-4485-8358-34502c871819" />


**Step 3**
Created new cluster in MongoDB Atlas and set the ConnectionString in .env file. Test the application with command "python app.py". And found it's working.
ImageName: **StudentRegistration**
<img width="1757" height="962" alt="image" src="https://github.com/user-attachments/assets/66247b72-7886-4dd9-8b35-b7eaec3d3f57" />


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
<img width="1457" height="271" alt="image" src="https://github.com/user-attachments/assets/04b311c7-4ee5-46ed-98e1-c6ee3af9b5c0" />

ImageName: **Cnfpytest**
<img width="1412" height="257" alt="image" src="https://github.com/user-attachments/assets/0e64a2e2-d100-4300-82be-c3d8c528345f" />

Run command python -m pytest -v and got the output 
ImageName: **CheckPytest**
<img width="1523" height="440" alt="image" src="https://github.com/user-attachments/assets/603ea6a8-3bb1-4c35-b65e-0d6fe1874917" />


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
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5deeb009-edc3-4fbe-a976-a793833e7bf5" />

**Step 9**
Build docker image
ImageName: **DockerImageCreated**
<img width="1502" height="540" alt="image" src="https://github.com/user-attachments/assets/0ce5302c-198e-49f8-95d4-244975a14cdf" />


Verify docker image 
Image named **flask-student-app** is listed.
ImageName: **DockerImageVerified**
<img width="1640" height="496" alt="image" src="https://github.com/user-attachments/assets/acc15465-23c4-4e33-a53b-bec554b83904" />





