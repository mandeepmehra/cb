pipeline {
   agent any
   tools { 
        maven 'maven3' 
        jdk 'jdk8' 
    }
   
    stages {
       stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }
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
