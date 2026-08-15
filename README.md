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

**Step 10**
Now run docker with container name flaskapp through command as below:
docker run -d -p 5000:5000 `
-e MONGO_URI="mongodb+srv://saurabhkumar2k_db_user:MPtTUMa09nop0Qbn@m0.lsqcivs.mongodb.net" `
-e SECRET_KEY="mysecretkey" `
--name flaskapp `
flask-student-app

After starting the container checking status with command as below:
docker ps
ImageName: **DockerRun**
<img width="1532" height="320" alt="image" src="https://github.com/user-attachments/assets/111c1dd1-0a2e-4226-b512-b8689f5d9465" />

**Step 11**
Now open application at http://localhost:5000
ImageName: **RunningApp**
<img width="1577" height="926" alt="image" src="https://github.com/user-attachments/assets/c8cf5e57-6e4b-4d18-8db1-a0f585ff4e25" />

It is confirmed that Dockerized Flask application is working successfully. 
So I have completed so far:
-Cloned repository
-Configured MongoDB Atlas
-Fixed .env configuration
-Application running locally
-Pytest executed successfully (4/4 passed)
-Docker image built
-Docker container running
-Application accessible at http://localhost:5000
-Code pushed to your GitHub repository

**Step 12**
**Need to go for AWS Setup**
Creating ECR repository
ImageName: **ECRRepo**
<img width="1887" height="940" alt="image" src="https://github.com/user-attachments/assets/ebce9961-308b-4e53-b98e-d7d2e3a26564" />

**Step 13**
Created EC2 instance
ImageName: **EC2Instance**
<img width="1870" height="882" alt="image" src="https://github.com/user-attachments/assets/81a0fc5b-33b3-4667-a21d-b5bfdbadfbaf" />

**Step 14**
Now installing Docker with commands
sudo apt update
ImageName: **DockerInstall**
<img width="1896" height="817" alt="image" src="https://github.com/user-attachments/assets/42152f89-be3e-4c76-8a72-7048e2de47ae" />
ImageName: **DockerVerify**
<img width="1738" height="438" alt="image" src="https://github.com/user-attachments/assets/97c5c317-50c6-4606-ad62-074f5380bd25" />


**Step 15**
IAM

Role Created
ImageName: **RoleCreated**
<img width="1901" height="953" alt="image" src="https://github.com/user-attachments/assets/8a0d20a8-10da-4442-b62c-f6059102c61d" />

Modify IAM Role
ImageName: **RoleModified**
<img width="1906" height="847" alt="image" src="https://github.com/user-attachments/assets/9afacf6e-18d7-4fb6-93e6-c8ef90a509b8" />

Verified IAM ROle
ImageName: **RoleVerified**
<img width="1907" height="807" alt="image" src="https://github.com/user-attachments/assets/8d22b760-3a53-4e04-ac8b-c5fa393df3a7" />

**Step 16**
Now login to ECR
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 985818273957.dkr.ecr.us-east-1.amazonaws.com

ImageName: **ECRLogin**
<img width="1912" height="627" alt="image" src="https://github.com/user-attachments/assets/aee6ee68-d7f2-4f7a-8d6f-942bc29d02f3" />

**Step 17**
Checking my ECR repository and found it is listed
ImageName: **ECRRepoList**
<img width="1902" height="815" alt="image" src="https://github.com/user-attachments/assets/aa2472fa-0dce-49a8-90f3-45a883ededcc" />

**Step 18**

Worked on GitHub Actions for Build DOcker Image for ECR
ImageName: BuildDockerImage
<img width="1913" height="962" alt="image" src="https://github.com/user-attachments/assets/66b9e575-7723-48b9-8f4d-e13b12a2a35f" />

**Step 19**
Connected EC2 Instance and confirm repository
ImageName: CnfRepoEc
<img width="1898" height="801" alt="image" src="https://github.com/user-attachments/assets/f378a89e-9ebd-47d8-9801-486eb330727e" />

**Step 20**
Updated CICD.yaml file with corrected code and updated Github Secrates with correct AWS access key information (Id, Key), Finally got running workflow like below:
ImageName: **WOrkFlowFinal**
<img width="1877" height="948" alt="image" src="https://github.com/user-attachments/assets/126f3a78-18a1-4677-97b1-7776a856be36" />

**Step 21**
Go to ECR Repository checked here for an image **latest**
ImageName: **ImageECR**
<img width="1886" height="796" alt="image" src="https://github.com/user-attachments/assets/15a5ebe4-592e-4eb8-8912-e2240345d0be" />

**Step 22**
Image is existing now at ECR Repository. So login to EC2 and tried to pull image
ImageName: PullImage
<img width="1910" height="865" alt="image" src="https://github.com/user-attachments/assets/7e2fecf9-7caf-404a-adbf-8a2210b1ef19" />

ImageName:**PulledFinalImage**
<img width="1897" height="905" alt="image" src="https://github.com/user-attachments/assets/948ab90e-099b-4d06-8338-48d1aa59bde1" />

**Step 23**
Now run container
ImageName: **RunContainer**
<img width="1912" height="605" alt="image" src="https://github.com/user-attachments/assets/7bd5aaa5-21c5-4e7c-85a1-b162f67e3746" />

**Step 24**
Now confirm whether the GitHub Action successfully pushed the Docker image to ECR.
ImageName: **PushedDockerImage**
<img width="1893" height="853" alt="image" src="https://github.com/user-attachments/assets/d3a77006-1f2b-4cc7-b43d-968be18b45ad" />

**Step 25**

ImageName: **RunningFromEC2**
<img width="1917" height="898" alt="image" src="https://github.com/user-attachments/assets/dc4f0410-69ba-4b6f-b95e-0e4847d492c2" />

ImageName: **RunningHostedApplication**
<img width="1897" height="925" alt="image" src="https://github.com/user-attachments/assets/34549b15-4632-4ddf-a1e5-6bba1505e464" />


**Step 26**
Next step is for Email Configuration. 
Updated CI-CD.Yaml with code below:
name: Build Docker Image

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3

      - name: Build Docker Image
        run: docker build -t student-registration-app -f flask_Practice/Dockerfile flask_Practice

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1

      - name: Login to Amazon ECR
        id: login-ecr
        uses: aws-actions/amazon-ecr-login@v2

      - name: Tag Docker Image
        run: |
          docker tag student-registration-app:latest 985818273957.dkr.ecr.us-east-1.amazonaws.com/student-registration-app:${{ github.sha }}
      - name: Push Docker Image
        run: |
          docker push 985818273957.dkr.ecr.us-east-1.amazonaws.com/student-registration-app:${{ github.sha }}
          
      - name: Send Success Email
        if: success()
        uses: dawidd6/action-send-mail@v3
        with:
          server_address: smtp.gmail.com
          server_port: 465
          secure: true
          username: ${{ secrets.SMTP_USERNAME }}
          password: ${{ secrets.SMTP_PASSWORD }}
          subject: "SUCCESS - Student Registration Deployment"
          to: ${{ secrets.NOTIFY_EMAIL }}
          from: GitHub Actions
          body: |
            Deployment Successful
            Repository: ${{ github.repository }}
            Branch: ${{ github.ref_name }}
            Commit SHA: ${{ github.sha }}
            ECR Repository: student-registration-app
            EC2 Target: EC2 Deployment Successful
            Run URL:
            https://github.com/${{ github.repository }}/actions/runs/${{ github.run_id }}
      - name: Send Failure Email
        if: failure()
        uses: dawidd6/action-send-mail@v3
        with:
          server_address: smtp.gmail.com
          server_port: 465
          secure: true
          username: ${{ secrets.SMTP_USERNAME }}
          password: ${{ secrets.SMTP_PASSWORD }}
          subject: "FAILED - Student Registration Deployment"
          to: ${{ secrets.NOTIFY_EMAIL }}
          from: GitHub Actions
          body: |
            Deployment Failed
            Repository: ${{ github.repository }}
            Branch: ${{ github.ref_name }}
            Commit SHA: ${{ github.sha }}
            Please review the workflow logs.
            Run URL:
            https://github.com/${{ github.repository }}/actions/runs/${{ github.run_id }}

    Push code to the repository. And change SMTP Pasword and UserName
    
    ImageName: **SMTP**
    <img width="1657" height="811" alt="image" src="https://github.com/user-attachments/assets/7536f151-f2d2-4b23-b20a-fd1d7df4dc96" />

    And Finally got successfully deployment email
    ImageName: **EmailDeployment**
    <img width="1847" height="945" alt="image" src="https://github.com/user-attachments/assets/7011f531-ebaa-4a54-8932-d6f50a317dc5" />

    










