pipeline {
	agent any         
		stages {                 
			stage('Prepare') {                         
				steps {                                 
					echo 'Preparing..'
				}                 
			}                 
			stage('Build') {                         
				steps {                                 
					echo 'Building..'
					sh 'docker build --rm . -t challengejenkins'                         
				}                 
			}                 
			stage('Test') {                         
				steps {                                 
					echo 'Testing...'  
					sh 'docker run challengejenkins npm test'                        
				}                 
			}
			stage('push') {
				steps {
					echo 'pushing'
					withCredentials([usernameColonPassword(credentialsId: 'ae6de152-f4b5-49e5-8f19-264f76b8bbf6', variable: 'DockerHub')]) {
						sh 'docker login'
					}
					sh 'docker tag challengejenkins:latest cristiancristancho/challengejenkins:latest'
					sh 'docker push cristiancristancho/challengejenkins:latest'

				}
			}                 
			stage('Deploy') {                         
				steps {                                 
					echo 'Deploying....'                                     					
				}                 
			}         
		} 
} 
