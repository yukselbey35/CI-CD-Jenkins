## DevOps Project for Beginners   

Now let us install Jenkins on the centos-host machine and configure it to run on port 8080 instead of the default port 8080.
You can refer to the Jenkins Installation Docs located above the terminal.

sudo yum install epel-release -y
sudo yum install java -y
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo --no-check-certificate
sudo rpm --import http://pkg.jenkins.io/redhat-stable/jenkins.io.key
sudo yum install jenkins -y

Edit /etc/sysconfig/jenkins file and change Jenkins port to 8090 by updating JENKINS_PORT variable value.
sudo vi /etc/sysconfig/jenkins

Once done start Jenkins service.
sudo systemctl start jenkins

How to integrate GitHub with Jenkins
First Install Git on Jenkins Instance: 
Second Install GitHub Plugin on Jenkins GUI: Because I want to integrate my Jenkins server with GitHub
Third Confiure Git on Jenkins GUI. Use Global Tool Configuration

Install Git on jenkins ssh: sudo yum install git -y
When we install any plugin we need to go to Dashboard and select Manage Jenkins > Manage Plugins>Install Github
TO Configure Git=> Global Tool Configuration Under Git section Patch executable write "git"
Because whenever we use git we shlould use git command


After configured git and github we will pull the code from github
So that we should create  NEW ITEM\
After installing and configuring GIT we have "Git" under the Source Code Managment 
We should set the repo url

When We click "Build Now" we build the job
Clone the repository successfuly. 

WHENEVER JENKINS DO BUILD ACTIVITY ITS DO UNDER THE workspace
/var/lib/jenkins/workspace/PullCodeFromGitHub

INTEGRATE MAVEN WITH JENKINS 
Setup Maven on Jenkins Server
Setup Environment Variables
 JAVA_HOME, M2, M2_HOME
we can see all these step under installing Apache Maven 
https://maven.apache.org/install.html
We need to download maven 
https://maven.apache.org/download.cgi
Select and download
Binary tar.gz archive	https://dlcdn.apache.org/maven/maven-3/3.8.4/binaries/apache-maven-3.8.4-bin.tar.gz
Use wget to download
wget https://dlcdn.apache.org/maven/maven-3/3.8.4/binaries/apache-maven-3.8.4-bin.tar.gz
Use tar to extract
tar -zxvf apache-maven-3.8.4-bin.tar.gz

We want to use maven with root because of that 
we will set the env variable under the .bash_profile

When we are setting we need to use jvm to find it 
find / -name java-11*
/usr/lib/jvm/java-11-openjdk-11.0.13.0.8-1.amzn2.0.3.x86_64

add to bash profile
vi .bash_profile 


M2_HOME=/opt/maven
M2=/opt/maven/bin
JAVA_HOME=/usr/lib/jvm/java-11-openjdk-11.0.13.0.8-1.amzn2.0.3.x86_64
# User specific environment and startup programs

PATH=$PATH:$HOME/bin:$JAVA_HOME:$M2_HOME:$M2


then use source command => source .bash_profile

we can use maven, and java from anywhere

Integrate Maven with Jenkins use GUI
Manage Jenkins > Manage Plugins Install the Maven Plugins
Then go to Global Tool Configuration to configure it.

Under the JDK section add these
java-11 
/usr/lib/jvm/java-11-openjdk-11.0.13.0.8-1.amzn2.0.3.x86_64

Under the Maven Section
Name and MAVEN_HOME
maven-3.8.4
/opt/maven

Then we will the careate the job
"Create a new job" means Click on "New Item"
When click on it we can see the create job options 
Free Style, Maven Project,  Pipeline, 

When we select Maven project using pom file to avoid some configuration
use source code managment and build options
give github repo url
and clean install
-------------------------------------------------------------------










