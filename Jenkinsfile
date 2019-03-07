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
					sh 'if [ "$(docker images ${reg} -q)" != "" ]; then docker rmi -f $(docker images ${reg} -q --no-trunc); fi'
					sh 'docker build --rm . -t challengejenkins:${BUILD_NUMBER}'                         
				}                 
			}                 
			stage('Test') {                         
				steps {                                 
					echo 'Testing...'  
					sh 'docker run --rm --name challjenkTest -d challengejenkins:${BUILD_NUMBER} npm test'                        
				}                 
			}
			
			stage('push') {
				steps {
					echo 'pushing'
					sh 'docker login -u $DockerUser -p $DockerPass'
					sh 'docker tag challengejenkins:${BUILD_NUMBER} cristiancristancho/challengejenkins:${BUILD_NUMBER}'
					sh 'docker push cristiancristancho/challengejenkins:${BUILD_NUMBER}'

				}
			}
			stage('Check') {                         
				steps {                                 
					echo 'Look the new version on port 8050....'  
					input 'check new version?'
					//sh 'docker stop $(docker ps -aq)'
					//sh 'docker rm $(docker ps -aq)'
					//sh 'docker rmi $( docker images | grep "^<none>" | awk "{print $3}" )'
					sh 'docker run --name challjenkNew -d -p 65000:8000 challengejenkins:${BUILD_NUMBER}'  
                                 					
				}                 
			}                  
			stage('Deploy') {                         
				steps {                                 
					echo 'Deploying....'  
					input 'Accept deployment?'
					//sh 'docker stop $(docker ps -aq)'
					sh 'docker stop challjenkNew'
					sh 'docker run --name challjenk -d -p 8000:8000 cristiancristancho/challengejenkins:latest'
                                 					
				}                 
			}         
		} 
} 
