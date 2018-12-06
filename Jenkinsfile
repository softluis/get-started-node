//def scannerHome = "C:\\Users\\0101547\\Downloads\\sonar-scanner-cli-3.2.0.1227-windows\\sonar-scanner-3.2.0.1227-windows" 
pipeline {
    agent any  
    stages{
        stage('Download Repository') {
            steps {
                checkout scm
            }
		}
        stage('Sonarqube') {
			
			steps {
					script{
               def scannerHome = tool 'Scanner'
			   echo scannerHome
    
                            withSonarQubeEnv('SonarServer') {
                                bat "\"${scannerHome}/bin/sonar-scanner \""
        }
		}
  }
}
	stage("Quality Gate") {
            steps {
			 timeout(time: 1, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: false
              }
				
        }
    }
	
	stage("Push IMB Cloud"){
		steps{
			echo 'Pushing to cloud'
		}
	}
}
}
