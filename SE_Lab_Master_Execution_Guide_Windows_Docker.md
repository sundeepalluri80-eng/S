# SE LAB MASTER EXECUTION GUIDE

## Windows + Docker Desktop \| Step-by-step practical runbook

This guide follows the task order in the uploaded Keshav Memorial
Institute SE Lab record. It covers every listed experiment and subtask.
Commands are labelled **PowerShell**, **Git Bash**, or **EC2 Ubuntu** so
you know where to run them.

Replace `USERNAME`, repository URLs, key names, paths and public IPs
with your own values. Do not publish passwords, private keys or access
tokens.

------------------------------------------------------------------------

# 0. PRE-LAB WINDOWS + DOCKER DESKTOP SETUP

## 0.1 Install the required software

Install StarUML, Git for Windows (Git Bash), JDK 11/17/21 as specified,
Apache Maven, Eclipse IDE for Enterprise Java and Web Developers, Tomcat
9, Docker Desktop, Minikube and kubectl. Install Jenkins using the
Windows MSI as in Task 5C, unless your lab permits the Docker option.

Create accounts at: - GitHub: https://github.com/ - Docker Hub:
https://hub.docker.com/ - AWS Academy: use your college invitation.

## 0.2 Docker Desktop first launch

1.  Download Docker Desktop for Windows from the official Docker
    website.
2.  Search Windows for **Turn Windows features on or off**.
3.  Enable **Virtual Machine Platform** and **Windows Subsystem for
    Linux**. Enable Hyper-V/Windows Hypervisor Platform if available and
    required by your Windows edition.
4.  Install Docker Desktop and restart if prompted.
5.  Open Docker Desktop, accept the licence and sign in.
6.  In Settings → General, enable the WSL 2 based engine if available.
7.  Wait until Docker Desktop says the engine is running.

If WSL installation is requested, open **PowerShell as Administrator**:

``` powershell
wsl --install
wsl --update
wsl --status
```

Restart if requested. Open Docker Desktop again.

## 0.3 Verify tools

Open a NEW PowerShell window:

``` powershell
git --version
java -version
javac -version
mvn -version
docker --version
docker compose version
docker info
```

If `docker info` says it cannot connect to the daemon, open Docker
Desktop and wait for Engine running.

## 0.4 Create a workspace

``` powershell
mkdir C:\SELab
cd C:\SELab
```

PowerShell navigation:

``` powershell
pwd
dir
mkdir folder-name
cd folder-name
cd ..
notepad filename
```

When saving `Dockerfile` or `docker-compose.yaml` in Notepad, choose
**Save as type: All files**. Do not accidentally create
`Dockerfile.txt`.

**Terminal choice** - PowerShell: Windows setup, Docker, Compose,
Minikube and Windows Jenkins commands. - Git Bash: Git practicals where
the record asks for Git Bash. - EC2 Ubuntu terminal: Linux commands only
after SSH login.

------------------------------------------------------------------------

# TASK 1 --- INSTALL STARUML, GIT BASH AND CREATE GITHUB ACCOUNT

## 1A. StarUML

1.  Search for StarUML and open its official website.
2.  Download the Windows installer.
3.  Run the downloaded setup file.
4.  Complete installation and open StarUML.
5.  Confirm the workspace opens.

## 1B. Git Bash

1.  Open the official Git for Windows download page.
2.  Download the Windows installer (normally 64-bit).
3.  Run the installer and complete setup.
4.  Open Git Bash from the Start menu.
5.  Verify:

``` bash
git --version
```

## 1C. GitHub account

1.  Open https://github.com/.
2.  Click Sign up.
3.  Enter email, username and password.
4.  Complete verification and sign in.
5.  Confirm the GitHub dashboard is visible.

------------------------------------------------------------------------

# TASK 2 --- IEEE SRS WITH UML DIAGRAMS

The record's sample is **ByteTickets**, an e-ticketing application with
**Ticket Cart** and **Ticket Transfer** features.

## 2A. Problem statement

Write that users face difficulty managing multiple tickets and
transferring tickets when plans change. ByteTickets solves this with a
cart to manage multiple tickets and a secure ticket-transfer feature.

## 2B. Prepare SRS document

Create a Word document and use these headings in order:

1.  Title page --- Software Requirement Specification for ByteTickets.
2.  Table of Contents.
3.  Introduction:
    -   Purpose
    -   Document conventions
    -   Intended audience and reading suggestions
    -   Product scope
    -   References
4.  Overall Description:
    -   Product perspective
    -   Product functions
    -   User classes and characteristics
    -   Operating environment
    -   Design and implementation constraints
    -   Assumptions and dependencies
5.  External Interface Requirements:
    -   User interface
    -   Hardware interface
    -   Software interface
    -   Communication interface
6.  System Features:
    -   Ticket Cart
    -   Ticket Transfer
    -   Description/priority
    -   Stimulus/response sequence
    -   Functional requirements
7.  Other Non-functional Requirements:
    -   Performance
    -   Safety
    -   Security
    -   Software quality attributes
    -   Business rules
8.  Other requirements and conclusion.

**Functional requirement examples** - System must allow users to add
multiple tickets to a cart. - System must show ticket count and total
price. - System must update the cart when tickets are added, removed or
quantities change. - System must allow a valid purchased ticket to be
transferred. - System must validate recipient details and update ticket
ownership. - System must notify sender and recipient of transfer status.

**Non-functional requirement examples** - Performance: common operations
should respond quickly. - Security: users must authenticate; ticket
transfers must be protected. - Reliability: purchases/transfers must not
corrupt ticket data. - Usability: simple interface for customers and
organizers. - Compatibility: support modern browsers and mobile
devices. - Maintainability: system should be easy to update.

## 2C. Draw UML diagrams in StarUML

**Start:** Open StarUML → create a new UML project → right-click
Model/Package → Add Diagram → select diagram type → drag elements from
toolbox → rename/connect → save.

### Use Case Diagram

1.  Add Use Case Diagram.
2.  Actors: Customer, Event Organizer, Administrator.
3.  Draw a system boundary named `ByteTickets`.
4.  Add use cases: Register/Login, Browse Events, Search Events, Add
    Ticket to Cart, View Cart, Purchase Ticket, View My Tickets,
    Transfer Ticket, Manage Events, Manage Users.
5.  Connect each actor to relevant use cases.

Notation: actor = stick figure; use case = oval; system boundary =
rectangle.

### Class Diagram

1.  Add Class Diagram.
2.  Add classes: User, Customer, EventOrganizer, Administrator, Event,
    Ticket, Cart, CartItem, Payment, TicketTransfer.
3.  Add a few attributes and operations to each class.
4.  Connect related classes with associations.
5.  Show inheritance from User to Customer/EventOrganizer/Administrator
    if using specialized user types.

Notation: class box has name, attributes and operations compartments.

### Sequence Diagram

1.  Add Sequence Diagram.
2.  Lifelines: Customer, ByteTickets UI, Ticket Service, Database,
    Notification Service.
3.  Draw messages from top to bottom:
    -   Customer selects a ticket.
    -   UI sends transfer request.
    -   Ticket Service validates ticket and recipient.
    -   Database updates ticket ownership.
    -   Notification Service sends confirmation.
    -   UI displays success/failure.

### Activity Diagram

1.  Add Activity Diagram.
2.  Draw initial node.
3.  Add actions: Login → Browse Events → Select Ticket → Add to Cart →
    Review Cart → Make Payment.
4.  Add decision: Payment successful?
5.  Yes → Generate e-ticket → Display confirmation.
6.  No → Display payment failure.
7.  Connect to final node.

Notation: initial = filled circle; action = rounded rectangle; decision
= diamond; final = bullseye.

## 2D. Save

Save the StarUML project and SRS document. Export diagrams if required
by the examiner.

------------------------------------------------------------------------

# TASK 3 --- INSTALL ECLIPSE, MAVEN, JDK, TOMCAT AND CONFIGURE TOMCAT

## 3A. JDK

1.  Install the JDK version required by the lab (11/17/21).
2.  Set `JAVA_HOME` to the JDK installation folder.
3.  Add `%JAVA_HOME%\bin` to Windows Path.
4.  Open a new PowerShell window.

``` powershell
java -version
javac -version
```

## 3B. Maven

1.  Download Apache Maven binary ZIP.
2.  Extract, e.g. to `C:\apache-maven`.
3.  Set `MAVEN_HOME` to that folder.
4.  Add `%MAVEN_HOME%\bin` to Path.
5.  Open a new PowerShell window.

``` powershell
mvn -version
```

## 3C. Eclipse

1.  Download Eclipse IDE for Enterprise Java and Web Developers.
2.  Install/launch Eclipse.
3.  Choose workspace, e.g. `C:\SELab\workspace`.

## 3D. Tomcat

1.  Download Tomcat 9 ZIP.
2.  Extract to `C:\apache-tomcat-9`.
3.  Start it:

``` powershell
cd C:\apache-tomcat-9\bin
.\startup.bat
```

4.  Open `http://localhost:8080` and verify the Tomcat page.
5.  Stop it:

``` powershell
.\shutdown.bat
```

## 3E. Configure Tomcat in Eclipse

1.  Eclipse → Window → Show View → Servers.
2.  Click the link to create a new server.
3.  Choose Apache → Tomcat v9.0 Server.
4.  Browse to `C:\apache-tomcat-9`.
5.  Select installed JDK → Finish.
6.  Right-click server → Start.
7.  Check Console for successful startup.

Compatibility: the record uses Servlet API 2.5 (`javax.servlet`); Tomcat
9 is the matching choice. Tomcat 10+ uses `jakarta.servlet` and may
require migration.

------------------------------------------------------------------------

# TASK 4 --- GIT COMMANDS

Use Git Bash for this task.

## 4A. Basic commands

``` bash
git --version
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global --list

mkdir -p ~/SELab/GitPractice
cd ~/SELab/GitPractice
git init
echo "Hello Git" > index.txt
git status
git add index.txt
git commit -m "First commit"
git diff
git log --oneline
git help
```

Meaning: version checks Git; config sets identity; init creates repo;
status shows changes; add stages; commit saves; diff shows changes; help
displays documentation.

## 4B. Branch, checkout, merge, revert, log

``` bash
git branch feature
git checkout feature
echo "Feature work" > feature.txt
git add .
git commit -m "Add feature"
git checkout main
git merge feature
git log --oneline
git revert HEAD
```

If your branch is `master`, use `master` instead of `main`. Rename it
with `git branch -M main`.

## 4C. Remote, clone, pull, push, fork

Create an empty GitHub repository and copy its HTTPS URL.

``` bash
git remote add origin https://github.com/USERNAME/REPOSITORY.git
git remote -v
git branch -M main
git push -u origin main
```

Clone and pull:

``` bash
git clone https://github.com/USERNAME/REPOSITORY.git
cd REPOSITORY
git pull origin main
```

Later push:

``` bash
git add .
git commit -m "Update files"
git push
```

Fork: 1. Open another user's repository on GitHub. 2. Click Fork →
select your account → Create Fork. 3. Copy your fork URL. 4. Clone your
fork using `git clone URL`.

Common errors: - `src refspec main does not match any`: create a commit
and check `git branch`. - `remote origin already exists`: use
`git remote -v`; correct URL with `git remote set-url origin URL`. -
Push rejected: `git pull --rebase origin main`, resolve conflicts, then
push. - GitHub HTTPS authentication uses browser/token sign-in, not the
account password.

------------------------------------------------------------------------

# TASK 5A --- CREATE MAVEN JAVA PROJECT IN ECLIPSE AND PUSH TO GITHUB

## 5A.1 Create project

1.  Eclipse → File → New → Maven Project → Next.
2.  Search `org.apache.maven`.
3.  Select `maven-archetype-quickstart`, version 1.4 or later as the
    record specifies.
4.  Group Id: `com.app`.
5.  Artifact Id: `JavaMaven`.
6.  Finish and wait for project creation.
7.  Open `pom.xml`.
8.  Open `src/main/java` → `com.app` → `App.java`.

Example program:

``` java
package com.app;

public class App {
    public static void main(String[] args) {
        System.out.println("Hello Maven Java Project");
    }
}
```

## 5A.2 Build in Eclipse

Right-click project → Run As: 1. Maven clean. 2. Maven install. 3. Maven
test. 4. Maven build.

For Maven Build goals enter:

``` text
clean install test
```

Click Apply → Run. Confirm `BUILD SUCCESS`.

Run program: right-click `App.java` → Run As → Java Application. Check
Console.

## 5A.3 Terminal build (alternative)

``` powershell
cd C:\path\to\JavaMaven
mvn clean
mvn install
mvn test
mvn package
```

## 5A.4 Push to GitHub

1.  GitHub → New repository → name `JavaMaven`.
2.  Select Maven `.gitignore` if offered.
3.  Create repository and copy HTTPS URL.
4.  Open Git Bash in the project folder:

``` bash
git init
git add .
git commit -m "Create Maven Java project"
git branch -M main
git remote add origin https://github.com/USERNAME/JavaMaven.git
git push -u origin main
```

5.  Refresh GitHub and verify files.

------------------------------------------------------------------------

# TASK 5B --- CREATE MAVEN WEB PROJECT IN ECLIPSE AND PUSH TO GITHUB

## 5B.1 Create project

1.  Eclipse → File → New → Maven Project → Next.
2.  Search `org.apache.maven`.
3.  Select `maven-archetype-webapp`, version 1.4 or later as in the
    record.
4.  Group Id: `com.app`.
5.  Artifact Id: `JavaMavenWebApp`.
6.  Finish and wait.

## 5B.2 Add Servlet API dependency

The record uses Servlet API 2.5. Add inside `dependencies` in `pom.xml`:

``` xml
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>servlet-api</artifactId>
    <version>2.5</version>
    <scope>provided</scope>
</dependency>
```

Keep the lab's specified dependency if its artifact differs.

## 5B.3 Edit JSP

Open `src/main/webapp/index.jsp`:

``` jsp
<html>
<body>
    <h1>Hello from Java Maven Web App</h1>
</body>
</html>
```

## 5B.4 Build and run

Right-click project → Run As → Maven clean, Maven install, Maven test,
Maven build. In Maven Build goals enter `clean install test`. Confirm
`BUILD SUCCESS` and WAR under `target`.

Then right-click project → Run As → Run on Server → select Tomcat 9 →
Finish. Open `http://localhost:8080/JavaMavenWebApp/`.

## 5B.5 Push to GitHub

Create repository `JavaMavenWebApp`, select Maven `.gitignore`, copy
HTTPS URL. In Git Bash at project folder:

``` bash
git init
git add .
git commit -m "Create Maven Web project"
git branch -M main
git remote add origin https://github.com/USERNAME/JavaMavenWebApp.git
git push -u origin main
```

Refresh GitHub to verify.

------------------------------------------------------------------------

# TASK 5C --- INSTALL JENKINS

## Method 1: Windows MSI (record procedure)

1.  Open https://www.jenkins.io/download/.
2.  Select Windows and download `jenkins.msi`.
3.  Run MSI → Next.
4.  Choose installation folder.
5.  Select Run service as LocalSystem if following the record.
6.  Test port 8080 to ensure it is free.
7.  Provide JDK path.
8.  Enable firewall exception.
9.  Install → Finish.
10. Open `http://localhost:8080`.
11. Open the initial admin password file at the path shown by installer.
12. Copy password into Jenkins.
13. Install suggested plugins.
14. Create admin user.
15. Set Jenkins URL to `http://localhost:8080/`.
16. Finish and open Dashboard.

Install record plugins: Manage Jenkins → Plugins → Available: - Maven
Integration - Build Pipeline - Pipeline Utility - Copy Artifact - Deploy
to Container

Manage Jenkins → Tools: 1. Add JDK and set its JDK path / JAVA_HOME. 2.
Add Maven and set Maven home / MAVEN_HOME. 3. Apply and Save.

## Method 2: Jenkins in Docker Desktop (use only if allowed)

PowerShell with Docker Desktop running:

``` powershell
docker volume create jenkins_home
docker run -d --name jenkins `
  -p 8080:8080 -p 50000:50000 `
  -v jenkins_home:/var/jenkins_home `
  jenkins/jenkins:lts
docker ps
docker logs jenkins
```

Open `http://localhost:8080`. Get password for the official Linux-based
image:

``` powershell
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

Complete setup. Configure JDK/Maven or use an agent that has them
installed. The Windows MSI is the record's method.

------------------------------------------------------------------------

# TASK 6A --- JENKINS FREESTYLE CI/CD FOR MAVEN JAVA

The record creates Build and Test jobs, then a Build Pipeline View.

## 6A.1 Build job

1.  Jenkins Dashboard → New Item.
2.  Name: `JavaMaven_Build`.
3.  Select Freestyle project → OK.
4.  Add description.
5.  Source Code Management → Git → paste Maven Java GitHub URL.
6.  Branch: `*/main` (or your actual branch).
7.  Build Steps → Invoke top-level Maven targets.
8.  Select configured Maven.
9.  Goals: `clean install`.
10. Post-build Actions → Archive the artifacts.
11. Files to archive: `**/*`.
12. Post-build Actions → Build other projects.
13. Project to build: `JavaMaven_Test`.
14. Select trigger only if build is stable.
15. Apply → Save.

## 6A.2 Test job

1.  Dashboard → New Item → `JavaMaven_Test` → Freestyle project.
2.  Build Environment → Delete workspace before build starts.
3.  Build Steps → Copy artifacts from another project.
4.  Project: `JavaMaven_Build`.
5.  Choose Latest Successful build / Stable build only if available.
6.  Artifacts to copy: `**/*`.
7.  Add Build Step → Invoke top-level Maven targets.
8.  Goals: `test`.
9.  Post-build Actions → Archive artifacts → `**/*`.
10. Apply → Save.

## 6A.3 Build Pipeline View

1.  Dashboard → click `+` beside views.
2.  Enter view name, e.g. `JavaMaven_Pipeline`.
3.  Select Build Pipeline View → Create.
4.  Upstream/Downstream configuration → select `JavaMaven_Build`.
5.  Apply → OK.
6.  Open the view and click Run/Build.
7.  Wait for Build and Test jobs.
8.  Open Console Output and verify success.

------------------------------------------------------------------------

# TASK 6B --- JENKINS FREESTYLE CI/CD FOR MAVEN WEB WITH POLL SCM

The record creates Build → Test → Deploy jobs.

## 6B.1 Verify web app on Tomcat

1.  Open Eclipse and Maven Web project.
2.  Right-click → Run As → Run on Server.
3.  Select Tomcat 9 → Finish.
4.  Confirm the web app opens.

## 6B.2 Build job

1.  Jenkins → New Item → `JavaMavenWebApp_Build` → Freestyle.
2.  Source Code Management → Git → paste web project GitHub URL.
3.  Branch: `*/main`.
4.  Build Triggers → Poll SCM.
5.  Schedule:

``` text
* * * * *
```

6.  Build Steps → Invoke top-level Maven targets.
7.  Goals: `clean install`.
8.  Post-build Actions → Archive artifacts → `**/*`.
9.  Post-build Actions → Build other projects → `JavaMavenWebApp_Test`.
10. Apply → Save.

## 6B.3 Test job

1.  New Item → `JavaMavenWebApp_Test` → Freestyle.
2.  Build Environment → Delete workspace before build starts.
3.  Build Steps → Copy artifacts from another project.
4.  Project: `JavaMavenWebApp_Build`.
5.  Artifacts to copy: `**/*`.
6.  Add Build Step → Invoke top-level Maven targets.
7.  Goals: `test`.
8.  Post-build Actions → Archive artifacts → `**/*`.
9.  Post-build Actions → Build other projects →
    `JavaMavenWebApp_Deploy`.
10. Apply → Save.

## 6B.4 Deploy job

1.  New Item → `JavaMavenWebApp_Deploy` → Freestyle.
2.  Build Environment → Delete workspace before build starts.
3.  Build Steps → Copy artifacts from another project.
4.  Project: `JavaMavenWebApp_Test`.
5.  Artifacts to copy: `**/*`.
6.  Post-build Actions → Deploy war/ear to a container.
7.  WAR/EAR files: `**/*.war`.
8.  Context path: `JavaMavenWebApp` (or actual project name).
9.  Container: Tomcat 9.
10. Add/select Tomcat credentials.
11. Apply → Save.

## 6B.5 Build Pipeline View and test

1.  Dashboard → `+` → Build Pipeline View.
2.  Name it `WebApp_Pipeline`.
3.  Create → Upstream/Downstream: select `JavaMavenWebApp_Build`.
4.  Apply → OK.
5.  Run pipeline and wait for Build → Test → Deploy.
6.  Open Tomcat Manager at the URL configured in your record (record
    shows `localhost:8082`).
7.  Log in using configured Tomcat Manager credentials.
8.  Verify the context path and application.

To test Poll SCM, commit/push a small change to GitHub and wait for the
next poll.

------------------------------------------------------------------------

# TASK 6C --- JENKINS SCRIPTED PIPELINE FOR MAVEN JAVA WITH POLL SCM

## 6C.1 Create Pipeline item

1.  Push Maven Java project to GitHub.
2.  Jenkins Dashboard → New Item.
3.  Name: `JavaMaven_ScriptedPipeline`.
4.  Select Pipeline → OK.
5.  In Build Triggers, the record's Maven pipeline section uses Build
    periodically with `* * * * *`. If your examiner specifically
    requires Poll SCM, select Poll SCM instead.

## 6C.2 Enter script

Pipeline → Definition: Pipeline script. Paste and replace URL/branch:

``` groovy
node {
    stage('Checkout') {
        git branch: 'main',
            url: 'https://github.com/USERNAME/JavaMaven.git'
    }

    stage('Build') {
        bat 'mvn clean install'
    }

    stage('Test') {
        bat 'mvn test'
    }

    stage('Complete') {
        echo 'Maven Java project build and test completed'
    }
}
```

The record's Jenkins installation is Windows, so `bat` is suitable for a
Windows agent. For a Linux agent, use `sh 'mvn clean install'` and
`sh 'mvn test'`.

## 6C.3 Run

1.  Apply → Save.
2.  Click Build Now.
3.  Open build number → Console Output.
4.  Verify Checkout, Build and Test stages succeed.
5.  Commit a small GitHub change.
6.  Wait for configured trigger and verify automatic execution.

------------------------------------------------------------------------

# TASK 7A --- INSTALL DOCKER, MINIKUBE AND CREATE DOCKER HUB ACCOUNT

## 7A.1 Docker Desktop

Follow Task 0.2. Then verify:

``` powershell
docker --version
docker info
```

## 7A.2 Docker Hub account

1.  Open https://hub.docker.com/.
2.  Click Sign Up.
3.  Enter details and verify email.
4.  Sign in and confirm dashboard.

## 7A.3 Minikube on Windows

Open PowerShell as Administrator:

``` powershell
New-Item -ItemType Directory -Force C:\minikube
$ProgressPreference = 'SilentlyContinue'
Invoke-WebRequest -OutFile C:\minikube\minikube.exe https://storage.googleapis.com/minikube/releases/latest/minikube-windows-amd64.exe
```

Add `C:\minikube` to PATH. Open a new terminal:

``` powershell
minikube version
kubectl version --client
```

Install kubectl if missing. Start Docker Desktop before Minikube.

------------------------------------------------------------------------

# TASK 7B --- DOCKER CLI COMMANDS

Open PowerShell after Docker Desktop says Engine running.

## 7B.1 Hello World

``` powershell
docker --version
docker pull hello-world
docker run hello-world
```

## 7B.2 List containers

``` powershell
docker ps
docker ps -a
```

## 7B.3 Remove container/image

Use actual IDs/names from `docker ps -a` and `docker images`:

``` powershell
docker rm CONTAINER_ID_OR_NAME
docker rmi IMAGE_NAME_OR_ID
```

## 7B.4 Redis

``` powershell
docker pull redis
docker run -d --name newredis redis
docker ps
docker exec -it newredis redis-cli
```

At Redis prompt:

``` text
SET name "SE Lab"
GET name
exit
```

Stop/start/remove:

``` powershell
docker stop newredis
docker start newredis
docker ps
docker stop newredis
docker rm newredis
docker rmi redis
```

------------------------------------------------------------------------

# TASK 7C --- MODIFY AND PUSH DOCKER IMAGE

The record modifies Ubuntu by installing Git, commits the changed
container as an image and pushes it to Docker Hub.

## 7C.1 Login and run Ubuntu

``` powershell
docker login -u YOUR_DOCKERHUB_USERNAME
docker pull ubuntu
docker run -it --name ubuntu-git ubuntu bash
```

## 7C.2 Install Git inside container

These commands run inside Ubuntu container:

``` bash
apt update
apt install git -y
git --version
exit
```

## 7C.3 Commit and push

Back in PowerShell:

``` powershell
docker ps -a
docker commit ubuntu-git YOUR_DOCKERHUB_USERNAME/ubuntu-git:latest
docker images
docker push YOUR_DOCKERHUB_USERNAME/ubuntu-git:latest
```

## 7C.4 Delete local copy, pull and verify

``` powershell
docker rm ubuntu-git
docker rmi YOUR_DOCKERHUB_USERNAME/ubuntu-git:latest
docker pull YOUR_DOCKERHUB_USERNAME/ubuntu-git:latest
docker run -it --name ubuntu-verify YOUR_DOCKERHUB_USERNAME/ubuntu-git:latest bash
```

Inside container:

``` bash
git --version
exit
```

Cleanup:

``` powershell
docker rm ubuntu-verify
docker rmi YOUR_DOCKERHUB_USERNAME/ubuntu-git:latest
docker logout
```

------------------------------------------------------------------------

# TASK 7D --- CREATE AND PUSH DOCKERFILE IMAGE

## 7D.1 Redis Dockerfile

``` powershell
mkdir C:\SELab\DockerProject1
cd C:\SELab\DockerProject1
mkdir redis
cd redis
notepad Dockerfile
```

Paste and save:

``` dockerfile
FROM redis:latest
CMD ["redis-server"]
```

Ensure the filename is exactly `Dockerfile`, not `Dockerfile.txt`.

## 7D.2 Build and run

``` powershell
docker build -t redisnew .
docker images
docker run -d --name redislatest redisnew
docker ps
docker exec -it redislatest redis-cli
```

Redis prompt:

``` text
SET name "Student"
GET name
exit
```

## 7D.3 Tag and push

``` powershell
docker login
docker tag redisnew YOUR_DOCKERHUB_USERNAME/redisnew:latest
docker push YOUR_DOCKERHUB_USERNAME/redisnew:latest
```

## 7D.4 Remove, pull and verify

``` powershell
docker stop redislatest
docker rm redislatest
docker rmi redisnew
docker pull YOUR_DOCKERHUB_USERNAME/redisnew:latest
docker run -d --name redis-pulled YOUR_DOCKERHUB_USERNAME/redisnew:latest
docker exec -it redis-pulled redis-cli
```

Test `SET` and `GET`, then:

``` powershell
docker stop redis-pulled
docker rm redis-pulled
docker rmi YOUR_DOCKERHUB_USERNAME/redisnew:latest
docker logout
```

## 7D.5 Calculator Dockerfile alternative shown in record

Create files:

``` powershell
mkdir C:\SELab\dockerCalculator
cd C:\SELab\dockerCalculator
notepad Calculator.js
```

`Calculator.js`:

``` javascript
const a = 20;
const b = 5;
console.log("Addition:", a + b);
console.log("Subtraction:", a - b);
console.log("Multiplication:", a * b);
console.log("Division:", a / b);
```

Create `Dockerfile`:

``` powershell
notepad Dockerfile
```

Paste:

``` dockerfile
FROM node:22
WORKDIR /app
COPY Calculator.js .
CMD ["node", "Calculator.js"]
```

Build/run/push:

``` powershell
docker build -t calculator .
docker run --name calculator-run calculator
docker login
docker tag calculator YOUR_DOCKERHUB_USERNAME/calculator:latest
docker push YOUR_DOCKERHUB_USERNAME/calculator:latest
```

Verify remote image:

``` powershell
docker rm calculator-run
docker rmi calculator
docker pull YOUR_DOCKERHUB_USERNAME/calculator:latest
docker run --name calculator-test YOUR_DOCKERHUB_USERNAME/calculator:latest
docker rm calculator-test
docker rmi YOUR_DOCKERHUB_USERNAME/calculator:latest
docker logout
```

------------------------------------------------------------------------

# TASK 7E --- MULTIPLE CONTAINERS USING DOCKER COMPOSE

The record uses WordPress + MySQL and opens WordPress at
`localhost:8000`.

## 7E.1 Create YAML

``` powershell
mkdir C:\SELab\compose
cd C:\SELab\compose
notepad docker-compose.yaml
```

Paste:

``` yaml
services:
  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: rootpass
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wpuser
      MYSQL_PASSWORD: wppass
    volumes:
      - dbdata:/var/lib/mysql

  wordpress:
    image: wordpress:latest
    restart: always
    ports:
      - "8000:80"
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: wppass
      WORDPRESS_DB_NAME: wordpress
    depends_on:
      - db

volumes:
  dbdata:
```

Save exactly as `docker-compose.yaml`.

## 7E.2 Validate and start

``` powershell
docker compose version
docker compose config
docker compose up -d
```

## 7E.3 Verify/open

``` powershell
docker ps -a
docker compose ps
```

Open `http://localhost:8000` and complete WordPress setup.

## 7E.4 Stop/start/remove

``` powershell
docker compose stop
docker compose start
docker compose stop
docker compose down
```

`docker compose down -v` also deletes the database volume/data; use only
if you intend to erase it.

YAML reminders: spaces, not tabs; consistent indentation; colon after
keys; quote port mapping `"8000:80"`; run Compose from the folder
containing the YAML. `docker compose config` checks syntax.

------------------------------------------------------------------------

# TASK 7F --- DEPLOY AND SCALE APPLICATIONS USING MINIKUBE

## 7F.1 Start Minikube

Start Docker Desktop first:

``` powershell
minikube start --driver=docker
minikube status
minikube ip
kubectl get nodes
```

## 7F.2 Create NGINX deployment

``` powershell
kubectl create deployment mynginx --image=nginx
kubectl get deployments
kubectl get pods
```

Wait for pod status `Running`.

## 7F.3 Expose service

``` powershell
kubectl expose deployment mynginx --type=NodePort --port=80 --target-port=80
kubectl get services
```

## 7F.4 Access the app

The record describes forwarding local port 8081 to container port 80.
Run:

``` powershell
kubectl port-forward service/mynginx 8081:80
```

Keep this terminal open and visit `http://localhost:8081`.

Alternative:

``` powershell
minikube service mynginx --url
```

Open the returned URL.

## 7F.5 Scale to four replicas

Open a second PowerShell terminal:

``` powershell
kubectl scale deployment mynginx --replicas=4
kubectl get deployments
kubectl get pods
```

Confirm four pods.

## 7F.6 Cleanup

``` powershell
kubectl delete service mynginx
kubectl delete deployment mynginx
minikube stop
```

Correction to a typo in the printed record: use
`kubectl delete service mynginx` to delete the service.

------------------------------------------------------------------------

# TASK 7G --- NAGIOS MONITORING USING DOCKER

## 7G.1 Login and pull

``` powershell
docker login
docker pull jasonrivers/nagios:latest
```

## 7G.2 Run container

``` powershell
docker run -d --name nagiosdemo -p 8888:80 jasonrivers/nagios:latest
docker ps
docker logs nagiosdemo
```

## 7G.3 Open Nagios

Visit `http://localhost:8888`.

The lab record gives: - Username: `nagiosadmin` - Password: `nagios`

Log in and inspect Nagios dashboard and Hosts view.

## 7G.4 Stop/remove/logout

``` powershell
docker stop nagiosdemo
docker rm nagiosdemo
docker rmi jasonrivers/nagios:latest
docker logout
```

------------------------------------------------------------------------

# TASK 8A --- AWS ACADEMY LEARNING ACCOUNT

1.  Open your college email and find the AWS Academy course invitation.
2.  Click Get Started.
3.  Click Create my account.
4.  Set password and select an Indian time zone.
5.  Accept required checkboxes and Register.
6.  Log out.
7.  Search/open AWS Academy login.
8.  Choose Student Login and sign in.
9.  Open AWS Academy Learner Lab → Modules.
10. Select AWS Academy Learner Lab.
11. Read terms and click I Agree.
12. Click Start Lab.
13. Wait until AWS indicator becomes green.
14. Click AWS to open AWS Console.
15. Open EC2.
16. When finished, return to Learner Lab → End Lab → Yes.

The record mentions a four-hour lab session; use the time/status shown
in your actual portal.

------------------------------------------------------------------------

# TASK 8B --- DEPLOY A PROJECT TO AWS USING EC2

## 8B.1 Launch instance

1.  Start AWS Academy Learner Lab and open AWS Console.
2.  Open EC2 → Launch instance.
3.  Enter instance name.
4.  Select Ubuntu AMI.
5.  Choose the eligible Free Tier instance shown in your lab.
6.  Architecture: 64-bit x86 as in the record.
7.  Instance type: record shows `t2.micro` (choose an available
    lab-eligible type).
8.  Create key pair: RSA, `.pem`; download and store securely.
9.  Network settings: allow HTTP and HTTPS as required.
10. Storage: record uses 8 GB.
11. Launch instance.
12. Wait for 2/2 status checks.

## 8B.2 Create static website locally

PowerShell:

``` powershell
mkdir C:\SELab\aws-static
cd C:\SELab\aws-static
notepad index.html
```

HTML:

``` html
<!DOCTYPE html>
<html>
<head><title>SE Lab AWS Deployment</title></head>
<body>
    <h1>Hello from AWS!</h1>
    <p>My Software Engineering Lab project is deployed.</p>
</body>
</html>
```

Save.

## 8B.3 Push static site to GitHub

Create an empty GitHub repository and copy HTTPS URL. Open Git Bash:

``` bash
cd /c/SELab/aws-static
git init
git add .
git commit -m "Add static website"
git branch -M main
git remote add origin https://github.com/USERNAME/aws-static.git
git push -u origin main
```

Verify `index.html` is visible on GitHub.

## 8B.4 SSH into EC2

In EC2 select instance → Connect → SSH client. Copy the example SSH
command. In PowerShell, go to the `.pem` folder and run:

``` powershell
cd C:\path\to\key
ssh -i .\your-key.pem ubuntu@YOUR_EC2_PUBLIC_IP
```

Accept host fingerprint if prompted.

## 8B.5 Install tools on EC2

These are **EC2 Ubuntu commands**:

``` bash
sudo apt update
sudo apt-get install docker.io -y
sudo apt install git nano -y
sudo systemctl enable --now docker
sudo docker --version
git --version
```

## 8B.6 Clone and create Dockerfile

``` bash
git clone https://github.com/USERNAME/aws-static.git
cd aws-static
nano Dockerfile
```

Paste:

``` dockerfile
FROM nginx:alpine
COPY . /usr/share/nginx/html
```

Save nano: Ctrl+O → Enter → Ctrl+X.

## 8B.7 Build and run

``` bash
sudo docker build -t my-web-app .
sudo docker run -d --name my-web-app -p 80:80 my-web-app
sudo docker ps
```

In EC2 Security Group inbound rules, allow HTTP TCP 80. Open:

``` text
http://YOUR_EC2_PUBLIC_IP
```

Confirm the web page loads.

## 8B.8 Cleanup

``` bash
sudo docker stop my-web-app
sudo docker rm my-web-app
```

Terminate EC2 only if the lab requires it: EC2 → Instance state →
Terminate instance. Wait for terminated state.

------------------------------------------------------------------------

# TASK 8C --- DEPLOY MAVEN WEB PROJECT TO AWS EC2

## 8C.1 Launch and connect

Repeat Task 8B.1: Start Learner Lab, launch Ubuntu EC2, create/download
RSA `.pem`, allow required traffic, wait for 2/2 checks and connect
using SSH.

## 8C.2 Install tools on EC2

``` bash
sudo apt update
sudo apt-get install docker.io -y
sudo apt install git nano -y
sudo systemctl enable --now docker
```

## 8C.3 Clone Maven Web repository

``` bash
git clone https://github.com/USERNAME/JavaMavenWebApp.git
cd JavaMavenWebApp
ls
```

Confirm `pom.xml` exists.

## 8C.4 Ensure WAR exists

The Dockerfile copies `target/*.war`, so a WAR must exist before the
Docker build. The record expects the Maven Web project and target WAR.

If building on EC2, install Maven/JDK and build:

``` bash
sudo apt install maven openjdk-17-jdk -y
mvn clean package
ls target
```

If building locally, ensure the WAR is transferred to EC2 or otherwise
included in the build context. A normal Git clone may not contain
`target` because build output is commonly ignored.

## 8C.5 Create record Dockerfile

``` bash
nano Dockerfile
```

Paste:

``` dockerfile
FROM tomcat:9-jdk21
COPY target/*.war /usr/local/tomcat/webapps/
```

Save: Ctrl+O → Enter → Ctrl+X.

## 8C.6 Build image

``` bash
sudo docker build -t maven-web-project .
sudo docker images
```

## 8C.7 Run Tomcat web app

Tomcat listens on port 8080 inside the container. Use this working port
mapping:

``` bash
sudo docker run -d --name maven-web-container -p 9090:8080 maven-web-project
sudo docker ps
sudo docker logs maven-web-container
```

In EC2 Security Group → Edit inbound rules → Add: - Type: Custom TCP -
Port range: `9090` - Source: your IP, or `0.0.0.0/0` temporarily for the
lab demo if required.

Open:

``` text
http://YOUR_EC2_PUBLIC_IP:9090/JavaMavenWebApp
```

Use the actual WAR/project context name if it differs.

**Record correction:** The printed run command says `-p 80:80`, but the
same record later opens port 9090 and Tomcat's default container port is
8080. `-p 9090:8080` matches Tomcat and the record's later
URL/security-group port.

## 8C.8 Stop and terminate

``` bash
sudo docker ps
sudo docker stop maven-web-container
sudo docker rm maven-web-container
```

Then terminate EC2 if instructed and wait for terminated state.

------------------------------------------------------------------------

# QUICK REVISION --- COMMANDS TO REMEMBER

## Git

``` bash
git --version
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git init
git status
git add .
git commit -m "message"
git branch
git checkout branch
git merge branch
git log --oneline
git revert HEAD
git remote -v
git clone URL
git pull origin main
git push -u origin main
```

## Maven

``` powershell
mvn -version
mvn clean
mvn compile
mvn test
mvn package
mvn install
```

## Docker

``` powershell
docker --version
docker pull IMAGE
docker images
docker run IMAGE
docker run -d --name NAME IMAGE
docker ps
docker ps -a
docker exec -it NAME sh
docker logs NAME
docker stop NAME
docker start NAME
docker rm NAME
docker rmi IMAGE
docker login
docker tag IMAGE USER/IMAGE:latest
docker push USER/IMAGE:latest
docker pull USER/IMAGE:latest
```

## Compose

``` powershell
docker compose version
docker compose config
docker compose up -d
docker compose ps
docker compose stop
docker compose start
docker compose down
```

## Minikube/Kubernetes

``` powershell
minikube start --driver=docker
minikube status
minikube ip
kubectl get nodes
kubectl create deployment mynginx --image=nginx
kubectl get deployments
kubectl get pods
kubectl expose deployment mynginx --type=NodePort --port=80 --target-port=80
kubectl scale deployment mynginx --replicas=4
kubectl get services
kubectl port-forward service/mynginx 8081:80
kubectl delete service mynginx
kubectl delete deployment mynginx
minikube stop
```

## EC2 Ubuntu (after SSH login)

``` bash
sudo apt update
sudo apt install docker.io git nano -y
sudo systemctl enable --now docker
git clone REPOSITORY_URL
sudo docker build -t IMAGE_NAME .
sudo docker run -d --name CONTAINER -p HOST_PORT:CONTAINER_PORT IMAGE_NAME
sudo docker ps
sudo docker logs CONTAINER
sudo docker stop CONTAINER
sudo docker rm CONTAINER
```

------------------------------------------------------------------------

# TROUBLESHOOTING

  -----------------------------------------------------------------------
  Problem                             First check
  ----------------------------------- -----------------------------------
  `docker` not recognized             Docker Desktop installed; reopen
                                      PowerShell; check PATH.

  Docker daemon unavailable           Start Docker Desktop; wait for
                                      Engine running.

  Docker Desktop won't start          Check virtualization, WSL 2 and
                                      Virtual Machine Platform; restart
                                      if required.

  Port already in use                 Stop conflicting service or choose
                                      another host port.

  Container name already exists       `docker ps -a`; remove old
                                      container if safe.

  Image will not delete               Remove containers using the image
                                      first.

  Docker Hub push denied              Check `docker login`, username,
                                      image tag and repository.

  Dockerfile not found                Change to folder containing exact
                                      `Dockerfile`; build with final `.`.

  File saved as `Dockerfile.txt`      Rename to `Dockerfile`; use Notepad
                                      Save as All files.

  Compose YAML invalid                Check spaces/indentation; run
                                      `docker compose config`.

  WordPress not loading               `docker compose ps` and
                                      `docker compose logs`.

  Minikube cannot start               Start Docker Desktop first; check
                                      `minikube status` and kubectl.

  Kubernetes pod not running          `kubectl get pods`;
                                      `kubectl describe pod POD_NAME`.

  Jenkins Maven build fails           Configure JDK/Maven in Manage
                                      Jenkins → Tools; ensure agent has
                                      them.

  Jenkins Git checkout fails          Verify repository URL, branch,
                                      credentials and network.

  WAR not found                       Run `mvn clean package`; verify
                                      `target/*.war`.

  EC2 site not opening                Check instance, public IP, running
                                      container and inbound
                                      security-group port.

  Tomcat EC2 URL not opening          Map host 9090 to container 8080;
                                      allow inbound TCP 9090.
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# FINAL PRACTICAL CHECKLIST

-   [ ] StarUML opens; Git Bash installed; GitHub account ready.
-   [ ] SRS document saved; UML diagrams saved/exported.
-   [ ] JDK, Maven, Eclipse and Tomcat versions verified.
-   [ ] Git init/add/commit/branch/merge/revert/remote/push/clone/pull
    practiced.
-   [ ] Maven Java project builds and is pushed to GitHub.
-   [ ] Maven Web project builds, runs on Tomcat 9 and is pushed to
    GitHub.
-   [ ] Jenkins installed; JDK/Maven/plugins configured.
-   [ ] Java Build/Test pipeline works.
-   [ ] Web Build/Test/Deploy pipeline and Poll SCM tested.
-   [ ] Scripted pipeline runs successfully.
-   [ ] Docker Desktop engine running.
-   [ ] Docker CLI and Redis commands practiced.
-   [ ] Modified Ubuntu image pushed and pulled from Docker Hub.
-   [ ] Redis/Calculator Dockerfile image built and pushed.
-   [ ] WordPress + MySQL Compose app opens at localhost:8000.
-   [ ] Minikube NGINX deployment scaled to four replicas.
-   [ ] Nagios dashboard opens at localhost:8888.
-   [ ] AWS Academy lab starts; EC2 SSH works.
-   [ ] Static site and Maven WAR deployment tested.
-   [ ] Lab containers stopped and EC2 terminated only as instructed.

------------------------------------------------------------------------

# PUSH THIS GUIDE TO YOUR GITHUB

After downloading this `.md` file, copy it into your existing cloned
GitHub repository folder. Open PowerShell in that repository and run:

``` powershell
git status
git add SE_Lab_Master_Execution_Guide_Windows_Docker.md
git commit -m "Add SE lab master execution guide"
git push origin main
```

If your default branch is `master`, use `git push origin master`.

To create a new GitHub repository: 1. GitHub → New repository → name it
`SE-Lab-Execution-Guide`. 2. Create it without adding a README or other
files. 3. Open PowerShell in the folder containing this Markdown file:

``` powershell
git init
git add SE_Lab_Master_Execution_Guide_Windows_Docker.md
git commit -m "Add SE lab master execution guide"
git branch -M main
git remote add origin https://github.com/USERNAME/SE-Lab-Execution-Guide.git
git push -u origin main
```

Replace `USERNAME` with your GitHub username and the URL with your
actual repository URL. Never commit `.pem` keys, passwords, tokens or
other secrets.
