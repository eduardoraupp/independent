def server
def rtMaven
def buildInfo
pipeline {
	agent any
	stages {
		stage("Build") {
			steps {
				script {
					println "HAS " + (params.isRelease != null)
					if(params.isParentRelease != null && params.isParentRelease) {
					//rtMaven.run pom: 'pom.xml', goals: 'clean'
					//rtMaven.run pom: 'pom.xml', goals: "scm:checkin -Dmessage=\"commiting the pom with the release version\" -DpushChanges=false"
					//release: -DreleaseVersion=0.0.5-SNAPSHOT -DdevelopmentVersion=0.0.6-SNAPSHOT					
					//	rtMaven.run pom: 'pom.xml', goals: '-B release:clean release:prepare release:perform'
						sh 'mvn -B release:clean release:prepare release:perform'
					//rtMaven.run pom: 'pom.xml', goals: 'clean install', buildInfo: buildInfo	
					} else {
					//	rtMaven.run pom: 'pom.xml', goals: 'clean install', buildInfo: buildInfo
						sh 'mvn clean install'					
					}
				}		
			}
		}
	}
}
