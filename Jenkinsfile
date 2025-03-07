pipeline {
	agent any
	stages {		
		
		stage ("CI Project"){
			steps {
				bat 'mvn clean install'
			}
			post {
			success {
			echo "Now Archiving ----"
			archiveArtifacts artifacts : '**/*.war'
				}
			}
		}
		stage ("Dev tomact Pipeline"){
			steps{
			build job : 'dev-tomact'
			}
		}
		stage ('Deploy to Production'){
            steps{
                timeout (time: 5, unit:'DAYS'){
                    input message: 'Approve PRODUCTION Deployment?'
                }
                
                build job : 'Declarative-jenkinsfile'
            }

            post{
                success{
                    echo 'Deployment on PRODUCTION is Successful'
                }

                failure{
                    echo 'Deployement Failure on PRODUCTION'
                }
            }
        }
	}
}
