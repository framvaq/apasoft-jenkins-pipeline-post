pipeline {
    agent any
   
    stages {
        stage('Create  directory for the WEB Application')
        {
            steps{
               
                //Fisrt, drop the directory if exists
                pwsh "rmdir -Force -r C:/proyectos/jenkins/directivas/tomcat-shopping"
                //Create the directory
                pwsh 'mkdir C:/proyectos/jenkins/directivas/tomcat-shopping'
                
            }
        }
        stage('Drop the Apache Tomcat Docker container'){
            steps {
            echo 'droping the container...'
            pwsh 'docker rm -f tomcat1'
            }
        }
        stage('Create the Tomcat container') {
            steps {
            echo 'Creating the container...'
            pwsh 'docker run -dit --name tomcat1 -p 9090:8080  -v C:/proyectos/jenkins/directivas/tomcat-shopping:/usr/local/tomcat/webapps tomcat:9.0'
            }
        }
        stage('Copy the web application to the container directory') {
            steps {
                echo 'Creating the shopping folder in the container'
                pwsh 'mkdir /home/jenkins/tomcat-web/shopping'
                echo 'Copying web application...'             
                pwsh 'cp -r shopping/* C:/proyectos/jenkins/directivas/tomcat-shopping/shopping'
            }
        }
    }

    post {
        success {
        // One or more steps need to be included within each condition's block.
        echo 'the deployment has worked'
       }
       failure {
        // One or more steps need to be included within each condition's block.
        echo 'An error has ocurred'
      }
 }
}
