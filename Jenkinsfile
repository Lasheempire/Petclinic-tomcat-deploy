pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                echo 'Checking out our code'
                git branch: 'main', url: 'https://github.com/Lasheempire/Petclinic-tomcat-deploy.git'
            }
        }

        stage('Test') {
            steps {
                echo "Running tests on our Maven build"
                sh "mvn clean test"
            }
        }

        stage('Build') {
            steps {
                echo "Packaging our project into a WAR file"
                sh "mvn clean install"
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying our WAR file into our Tomcat prod server"
                sshagent(['tomcat-pipeline']) {
                    sh "scp -o StrictHostkeyChecking=no target/petclinic.war tomcat@45.55.48.19:/opt/tomcat/webapps"
                }
            }
        }
    }
}
