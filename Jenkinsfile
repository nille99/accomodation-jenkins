pipeline {
    agent any 
    stages{
        stage('Checkout'){
            steps{
                checkout scm
            }
        }
     //Bulding the web-app
     stage('Build web-app'){
            steps{
                sh 'mvn -f /home/robot/.jenkins/workspace/test-jenkins-pipeline/hoteljsf clean install'
            }
        }
      //Bulding the web-service
     stage('Build web-service'){
            steps{
                sh 'mvn -f /home/robot/.jenkins/workspace/test-jenkins-pipeline/hotel-restfull clean install'
            }
        }
    //Deploy the artifacts on glassfish
     stage('Deploy the artifacts'){
            steps{
               sh 'asadmin deploy --force=true /home/robot/.jenkins/workspace/test-jenkins-pipeline/hotel-restfull/target/hotel-rest.war'
                sh 'asadmin deploy --force=true /home/robot/.jenkins/workspace/test-jenkins-pipeline/hoteljsf/target/hotel.war'
            }
        }
     //Clean databas
     stage('Clean databas'){
            steps{
               sh 'psql -h localhost -U postgres hotel -f /home/robot/.jenkins/workspace/test-jenkins-pipeline/hoteljsf/database-backup.sql'
            }
        }

    }
}
