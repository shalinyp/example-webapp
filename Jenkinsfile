def builderImage
def productionImage
def ACCOUNT_REGISTRY_PREFIX
def GIT_COMMIT_HASH

pipeline {
environment {
    registry = "shalinyp/example-webapp"
    registryCredential = 'munich'
    dockerImage = ''
  }
    agent any
    stages {
        stage('Checkout Source Code and Logging Into Docker hub') {
              steps{
				script {
					docker.build registry + ":$BUILD_NUMBER"
				}
			}
				
		}
		stage('Deploy Image') {
			steps{
			  script {
				  docker.withRegistry( '', registryCredential ) {
				  dockerImage.push()
              }
            }
			}
        }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}

