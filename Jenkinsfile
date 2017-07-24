node('vagrant-vm'){
   def mvnHome
   stage('git clone') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/samit2040/carthage.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
     // mvnHome = tool 'M3'
   }
   stage('Build') {
          // Run the maven build
        try{
          if (isUnix()) {
            sh "mvn  package"
            //sh "mvn -Dmaven.test.failure.ignore clean package"
            }
          }catch(err){
                archive '**/target/*.war'
                junit '**/target/surefire-reports/*.xml'
                throw err
            }
       }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive '**/target/*.war'
   }
   stage('publishDockerImage') {
      // Run the maven build
      if (isUnix()) {
         sh "./buildDockerImage.sh 12"
      }
   }
}