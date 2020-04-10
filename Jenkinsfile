pipeline {
    agent any
    stages{
        stage('Build'){
           steps{
               sh 'mvn clean package''
           }    
           post {
               success{
                   echo 'start store...'
                   archiveArtifacts artifacts: '**/target/*.war''
           }
       }
    }
  }  
}
