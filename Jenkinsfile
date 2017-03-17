node {
   def mvnHome
   def version
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/beingpratik/addressbook.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.
      mvnHome = tool 'LOCAL_MAVEN'
      version='2.3.5'
   }
   stage('UNITTEST') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore test -Pfunctional-test -DSkipUTs=true -DskipTests=true"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
     stage('Unti test report') {
      junit '**/target/surefire-reports/TEST-*.xml'
      
   }

   stage('PMD') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' pmd:pmd"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }

   stage('Cobertura') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' cobertura:cobertura"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Publish cobertura Reports') {
      publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'addressbook_main/target/site/cobertura/', reportFiles: 'index.html', reportName: 'HTML Report'])

   }


  
   
}

