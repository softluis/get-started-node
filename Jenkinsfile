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
			
			 environment{
					
               scannerHome = tool 'Scanner'
			   
			   }
			   steps {
					withSonarQubeEnv('SonarServer') {
                          bat "\"${scannerHome}/bin/sonar-scanner\""
        
		}
  }
}
	stage("Quality Gate") {
            steps {
				retry(2){
			script{
			   timeout(time: 5, unit: 'MINUTES') {
       def qg = waitForQualityGate()
       if(qg.status == "ERROR"){
            echo "Failed Quality Gates";
       }
       if (qg.status == 'OK') {
         echo "Passed Quality Gates!";
       }
    
    }
	}
	}
	}
	}
	stage("Push IMB Cloud"){
		steps{
			echo 'Pushing to cloud'
            pushToCloudFoundry(
                    target: 'https://api.eu-gb.bluemix.net',
                    organization: 'luis.filipe.pereira@pt.softinsa.com',
                    cloudSpace: 'dev',
                    credentialsId: 'imbcloud'
)
		}
	}
}
		post {
		always {
		 slackSend message
		}
		}
}
