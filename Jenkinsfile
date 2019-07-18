pipeline {

	agent any
	environment {
		MVN_HOME = '/opt/maven'
		def pom = readMavenPom file: 'pom.xml'
	}
			stages{
   
		stage('checkout') {
				steps {
					checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/rashmi7321/java-1.git']]])
				}
          
			}
			stage('Build') {
				steps { 
					sh "mvn clean install"
				}
			}

			stage("publish to nexus") {
			  stage('UploadToNexus'){
				steps {
					nexusPublisher nexusInstanceId: 'nexusrepo', nexusRepositoryId: 'sample', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: 'target/ROOT.war']], mavenCoordinate: [artifactId: 'sample', groupId: 'maven', packaging: 'war', version: '$BUILD_NUMBER']]]
				}
			}
 
         }
    }
}
