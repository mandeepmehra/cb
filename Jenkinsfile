pipeline {
   agent any
   tools { 
        mvn 'maven3' 
        jdk 'jdk8' 
    }
    stages {
       stage ('Checkout'){
          steps{
             checkout scm
          }
       }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
    }
}
