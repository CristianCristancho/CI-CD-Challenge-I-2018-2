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
					withCredentials([usernameColonPassword(credentialsId: '755fbb27-d3be-40c6-9af4-430379b9f94a', variable: 'Credentials')]) {
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
