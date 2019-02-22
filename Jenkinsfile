pipeline {
	agent any
		environment {
			DockerUser = credentials('DockerUser')
			DockerPass = credentials('DockerPass')
		}
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
					sh 'docker login -u $DockerUser -p $DockerPass'
					sh 'docker tag challengejenkins:latest cristiancristancho/challengejenkins:latest'
					sh 'docker push cristiancristancho/challengejenkins:latest'

				}
			}                 
			stage('Deploy') {                         
				steps {                                 
					echo 'Deploying....'  
					sh 'docker rm -f challengejenkins'
					input 'Start deployment? '
					sh 'docker run -d -p 8000:8000 challengejenkins npm start'  
					input 'Finish deployment? '
					sh 'docker stop challengejenkins'                                 					
				}                 
			}         
		} 
} 
