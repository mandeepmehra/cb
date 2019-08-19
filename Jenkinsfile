pipeline {
   agent any
   tools { 
        maven 'Maven 3' 
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
