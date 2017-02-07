node {
   // Mark the code checkout 'stage'....
   stage 'Checkout'

   // Checkout code from repository
   checkout scm

   
   stage 'Build'
   // Get the maven tool.
   // ** NOTE: This 'M3' maven tool must be configured
   // **       in the global configuration.
   def mvnHome = tool 'M3'
   // Run the maven build
   sh "${mvnHome}/bin/mvn clean install"

   stage 'Deploy'
   
   xlrCreateRelease serverCredentials: 'xlrelease', startRelease: true, template: 'Test', variables: [[propertyName: 'buildUrl', propertyValue: '${BUILD_URL}']], version: 'Release for $BUILD_TAG'
   
   sh 'export'
   //input id: 'DEPLOY', message: 'Proceed for deployment ?', submitter: 'xlrelease'

  // Do something
}
