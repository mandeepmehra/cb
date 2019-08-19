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
                def server = Artifactory.server 'local-artifactory'
                def uploadSpec = """{
                    "files": [
                        {
                        "pattern": "target/*.jar",
                        "target": "libs-snapshot-local/petclinic/"
                        }
                    ]
                    }"""
                def buildInfo = server.upload(uploadSpec)
                server.publishBuildInfo buildInfo
                echo buildInfo.name
                def promotionConfig = [
                    // Mandatory parameters
                    'buildName'          : 'cb :: master',
                    'buildNumber'        : 10,
                    'targetRepo'         : 'libs-release-local',
                
                    // Optional parameters
                    'comment'            : 'this is the promotion comment',
                    'sourceRepo'         : 'libs-snapshot',
                    'status'             : 'Released',
                    'includeDependencies': true,
                    'copy'               : true,
                    // 'failFast' is true by default.
                    // Set it to false, if you don't want the promotion to abort upon receiving the first error.
                    'failFast'           : true
                ]
                
                // Promote build
                server.promote promotionConfig

             }
          }
       }
    }
}
