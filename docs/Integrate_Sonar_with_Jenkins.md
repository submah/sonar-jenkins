<img src="../images/c4logo.png">

### Steps:
1. Login to your Linux VM and [Install docker](https://github.com/submah/docker-tutorials/edit/master/install_docker_centos7.md).

2. Create Two Docker Volumes to persist Jenkins and Sonar data
    
    * docker volume create sonar-data
    
    * docker volume create jenkins-data

3. Launch Container based Sonar [Click Here to see the steps](https://github.com/submah/sonar-jenkins/blob/main/docs/ting_up_a_Dockerized_SonarScanner.md)

4. Launch Container based Jenkins with below command.

    * docker run -d -p 8080:8080 -p 50000:50000 --name=jenkins -v jenkins-data:/var/jenkins_home jenkins/jenkins:lts

    #### To get the login password

    * cat /var/lib/docker/volumes/jenkins-data/_data/secrets/initialAdminPassword

5. To access jenkins Web UI Navigate to linux_Host_IP:8080. Default UserName is **admin** and Password is **refer To get the login password**

6. To Install the SonarScanner Pluging, Navigateto 
   
   Manage Jenkins >> Manage Plugins >> Available Tab >> Search for **SonarQube Scanner for Jenkins** >> Install the Plugin >> restart the Jenkins.

7. 