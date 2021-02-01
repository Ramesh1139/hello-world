pipeline {
    agent any
    environment {
        PATH = "/opt/maven/bin:$PATH"
    }
    stages {
        stage("clone code"){
            steps{
               git credentialsId: 'git_credentials', url: 'https://github.com/Ramesh1139/hello-world.git'
            }
        }
        stage("build code"){
            steps{
              sh "mvn clean install"
            }
        }
        stage("deploy"){
            steps{
              sshagent(['deploy_user']) {
                 sh "scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@10.0.2.183:/opt/tomcat/webapps"
                 
                }
            }
        }
    }
}
