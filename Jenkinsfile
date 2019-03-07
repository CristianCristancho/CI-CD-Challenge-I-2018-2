pipeline {
	agent any
		/*
		environment {
			DockerUser = credentials('DockerUser')
			DockerPass = credentials('DockerPass')
		}*/
		stages {                 
			stage('Prepare') {                         
				steps {                                 
					echo 'Preparing..'
				}                 
			}                 
			stage('Build') {                         
				steps {                                 
					echo 'Building..'
					sh 'docker build --rm . -t challengejenkins:new'                         
				}                 
			}                 
			stage('Test') {                         
				steps {                                 
					echo 'Testing...'  
					sh 'docker run challengejenkins:new npm test'                        
				}                 
			}
			/*
			stage('push') {
				steps {
					echo 'pushing'
					sh 'docker login -u $DockerUser -p $DockerPass'
					sh 'docker tag challengejenkins:latest cristiancristancho/challengejenkins:latest'
					sh 'docker push cristiancristancho/challengejenkins:latest'

				}
			}*/
			stage('Check') {                         
				steps {                                 
					echo 'Look the new version on port 8050....'  
					input 'check new version?'
					//sh 'docker stop $(docker ps -aq)'
					//sh 'docker rm $(docker ps -aq)'
					sh 'docker run -d -p 8050:8000 challengejenkins:new'  
                                 					
				}                 
			}                  
			stage('Deploy') {                         
				steps {                                 
					echo 'Deploying....'  
					input 'Accept deployment?'
					//sh 'docker stop $(docker ps -aq)'
					sh 'docker stop challengejenkins:new'
					sh 'docker rename challengejenkins:new challengejenkins:actual'
					sh 'docker rm challengejenkins:new'
					sh 'docker run -d -p 8000:8000 challengejenkins:actual'  
                                 					
				}                 
			}         
		} 
} 
