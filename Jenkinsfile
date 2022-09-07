pipeline {
  agent any
   tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven"
   }
  stages {
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            checkout([$class: 'GitSCM', branches: [[name: 'origin/jenkins-test-2']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Cynthiaa-18/Common']]])
             bat "mvn -Dmaven.test.failure.ignore=true clean package"
          }
       post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
       }
        }
      }
    }
	}
}

