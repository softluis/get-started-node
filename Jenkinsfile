def scannerHome = "C:\\Users\\0101547\\Downloads\\sonar-scanner-cli-3.2.0.1227-windows\\sonar-scanner-3.2.0.1227-windows" 
def qg = waitForQualityGate()
pipeline {
    agent any  
    stages{
        stage('Download Repository') {
            steps {
                checkout scm
            }
		}
        stage('Sonarqube') {
            environment {
                scannerHome = tool 'Scanner'
    }
                        steps {
                            withSonarQubeEnv('SonarServer') {
                                bat "${scannerHome}/bin/sonar-scanner "
        }
  }
}
	stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'MINUTES') { 
				if (qg.status != 'OK') {
             error "Pipeline aborted due to quality gate failure: ${qg.status}"
           }
        }
    }
	}
}
}
