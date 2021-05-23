pipeline {
    agent any
    environment {
        PATH = "/root/maven/bin:$PATH"
    }
    stages {
        stage("clone code"){
            steps{
               git credentialsId: 'git_credentials', url: 'https://github.com/kotapatai/project-valaxy.git'
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
                 sh "scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@13.233.197.93:/root/apache-tomcat-8.5.66/webapps"
                 
                }
            }
        }
    }
}
