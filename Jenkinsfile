pipeline {
   agent any
   tools { 
        maven 'mvn' 
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
       stage('Upload') {
          steps {
             script{
                def uploadSpec = """{
                    "files": [
                        {
                        "pattern": "target/*.jar",
                        "target": "libs-snapshot-local/petclinic/"
                        }
                    ]
                    }"""
                server.upload(uploadSpec)
             }
          }
       }
    }
}
