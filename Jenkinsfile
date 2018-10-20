node {
   def mvnHome
   stage('Preparation') { // for display purposes
      git 'https://github.com/eduardoraupp/independent.git'
      mvnHome = tool 'M3'
   }
   stage('Build') {
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Results') {
      archive 'target/*.jar'
   }
   stage('Release') {
       
   }
}
