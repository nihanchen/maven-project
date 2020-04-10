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
                   echo 'start store....'
                   archiveArtifacts artifacts: '**/target/*.war'
                }
           }
       }
       stage('deploy to staging'){
           steps{
               build job:'deploy-to-staging'
           }
       }
       stage('deploy to production')
           steps{
               timeout(time:5, unit:'DAYS'){
                   input message: '是否部署到生产环境'
               }
               build job: 'deploy-to-production'
           }
           post{
               success{
                   echo '部署到生产环境'
               }
               failture{
                   echo '部署失败'
               }
           }
    }  
}
