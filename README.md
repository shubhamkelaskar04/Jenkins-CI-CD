# Jenkins CI/CD Pipeline

## Project Overview

This project demonstrates a **Continuous Integration and Continuous Deployment (CI/CD) pipeline** using Jenkins.
The pipeline automatically:

* Pulls source code from GitHub
* Builds the project using Maven
* Runs automated tests
* Deploys the generated JAR file

The setup is performed on a **Windows local system**.

---

# Technologies Used

* Jenkins
* Apache Maven
* Java JDK 17
* Git
* GitHub

---

# Project Structure

```
Jenkins-CI-CD
│
├── src
│   └── test
│       └── java
│           └── AppTest.java
│
├── pom.xml
├── Jenkinsfile
└── README.md
```

---

# Prerequisites

Install the following tools:

### 1. Java JDK

Install **JDK 17**.

Verify installation:

```
java -version
javac -version
```

---

### 2. Apache Maven

Verify Maven installation:

```
mvn -version
```

---

### 3. Git

Verify Git installation:

```
git --version
```

---

### 4. Jenkins

Start Jenkins and open:

```
http://localhost:8080
```

---

# Jenkins Configuration

## Configure Git

1. Go to:

```
Manage Jenkins → Global Tool Configuration
```

2. Under **Git**, verify installation.

Example path:

```
C:\Program Files\Git\bin\git.exe
```

---

## Configure Maven

1. Open:

```
Manage Jenkins → Global Tool Configuration
```

2. Under **Maven**:

```
Name: Maven
MAVEN_HOME: C:\Program Files\Apache\Maven
```

---

## Configure JDK

1. Go to:

```
Manage Jenkins → Global Tool Configuration
```

2. Under **JDK**:

```
Name: JDK17
JAVA_HOME: C:\Program Files\Eclipse Adoptium\jdk-17
```

---

# Creating the Jenkins Pipeline Job

1. Click **New Item**
2. Enter name:

```
CI-CD-Pipeline
```

3. Select:

```
Pipeline
```

4. Under **Pipeline Definition** choose:

```
Pipeline script from SCM
```

5. Configure SCM:

```
SCM: Git
Repository URL: https://github.com/your-username/Jenkins-CI-CD.git
Branch: main
Script Path: Jenkinsfile
```

---

# Jenkinsfile

```
pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/your-username/Jenkins-CI-CD.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                bat '''
                if not exist C:\\deploy mkdir C:\\deploy
                copy target\\jenkins-demo-1.0.jar C:\\deploy
                '''
            }
        }

    }
}
```

---

# Pipeline Stages Explained

### 1. Clone Code

Jenkins pulls the latest source code from GitHub.

### 2. Build

Maven compiles the project and generates a **JAR file**.

```
mvn clean install
```

---

### 3. Run Tests

JUnit test cases are executed.

```
mvn test
```

---

### 4. Deploy

The generated JAR file is copied to the deployment folder.

```
C:\deploy
```

---

# Running the Pipeline

1. Open Jenkins
2. Select the pipeline job
3. Click:

```
Build Now
```

---

# Expected Pipeline Flow

```
GitHub Repository
        ↓
Jenkins Pipeline
        ↓
Clone Source Code
        ↓
Build using Maven
        ↓
Run Unit Tests
        ↓
Deploy JAR File
```

---

# Deployment Output

After successful execution, the JAR file will be available at:

```
C:\deploy
```

Example:

```
jenkins-demo-1.0.jar
```

---

# Sample Jenkins Console Output

```
Stage: Build
BUILD SUCCESS

Stage: Run Tests
Tests run: 1, Failures: 0

Stage: Deploy
1 file(s) copied

Finished: SUCCESS
```

---

# Conclusion

This project demonstrates a basic **CI/CD pipeline using Jenkins and Maven** that automatically builds, tests, and deploys a Java application whenever changes are pushed to GitHub.

---

# Author

Shubham Kelaskar
