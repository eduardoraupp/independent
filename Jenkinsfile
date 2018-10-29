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
						sh 'mvn -B release:clean release:prepare release:perform'
					} else {
						sh 'mvn clean install'					
					}
				}		
			}
		}
	}
}
