pipeline {
   agent any
   tools { 
        maven 'maven3' 
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
