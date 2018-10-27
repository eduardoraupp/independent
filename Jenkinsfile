def server
def rtMaven
def buildInfo
pipeline {
	agent any
	stages {
		stage("Artifactory") {
			steps {
				script {
					server  = Artifactory.server 'artifactory'
					rtMaven = Artifactory.newMavenBuild()
					rtMaven.tool = 'M3'
					rtMaven.deployer releaseRepo: 'libs-release-local', snapshotRepo: 'libs-snapshot-local', server: server
					rtMaven.resolver releaseRepo: 'libs-release', snapshotRepo: 'libs-snapshot', server: server
					rtMaven.deployer.artifactDeploymentPatterns.addExclude("pom.xml")
					buildInfo = Artifactory.newBuildInfo() 
					buildInfo.retention maxBuilds: 10, maxDays: 7, deleteBuildArtifacts: true
					buildInfo.env.capture = true
				}			
			}
		}
		stage("Build") {
			steps {
				script {
					println "HAS " + (params.isRelease != null)
					if(params.isRelease != null && params.isRelease) {
					//rtMaven.run pom: 'pom.xml', goals: 'clean'
					rtMaven.run pom: 'pom.xml', goals: "scm:checkin"
					rtMaven.run pom: 'pom.xml', goals: '-B release:prepare release:perform -X'
					//rtMaven.run pom: 'pom.xml', goals: 'clean install', buildInfo: buildInfo	
					} else {
						rtMaven.run pom: 'pom.xml', goals: 'clean install -X', buildInfo: buildInfo
					}
				}		
			}
		}
		stage('Publish build info') {
			steps {
				script {
					server.publishBuildInfo buildInfo
				}
			}
		}
	}
}
