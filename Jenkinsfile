pipeline {
    agent any
    tools{
        maven 'local maven'
    }

    stages{
        stage('Build'){
           steps{
               sh 'mvn clean package'
           }    
           post {
               success{
                   echo 'start store...'
                   archiveArtifacts artifacts: '**/target/*.war'
                }
           }
       }
       
       stage('deploy to staging'){
           steps{
               build job:'deploy-to-staging-project'
           }
       }
       /*
       stage('deploy to production'){
           steps{
               timeout(time:5, unit:'DAYS'){
                   input message: 'deploy to production or not'
               }
               build job: 'deploy-to-production-project'
           }
           post{
               success{
                   echo 'deployment successful'
               }
               failure{
                   echo 'deployment failure'
               }
           }
       }
       */
    }  
    
}
