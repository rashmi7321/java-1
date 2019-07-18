pipeline {

	agent any
	environment {
		MVN_HOME = '/usr/share/apache-maven'
	}
			stages{
   
		stage('checkout') {
				steps {
					checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/rashmi7321/java-1.git']]])
				}
          
			}
			stage('Build') {
				steps { 
					sh "'${MVN_HOME}/bin/mvn' clean package"
				}
			}

			stage('UploadToNexus'){
				steps {
					nexusPublisher nexusInstanceId: 'nexusrepo', nexusRepositoryId: 'sample', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: 'target/ROOT.war']], mavenCoordinate: [artifactId: 'sample', groupId: 'maven', packaging: 'war', version: '$BUILD_NUMBER']]]
				}
			}
    }
}
