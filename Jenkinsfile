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
					sh 'docker build --rm . -t challengejenkins'
					sh 'if [ "$(docker images ${reg} -q)" != "" ]; then docker rmi -f $(docker images ${reg} -q --no-trunc); fi'
				}                 
			}                 
			stage('Test') {                         
				steps {                                 
					echo 'Testing...'  
					sh 'docker run --rm --name challjenkTest -d challengejenkins npm test'                        
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
					//sh 'docker rmi $( docker images | grep "^<none>" | awk "{print $3}" )'
					sh 'docker run --rm --name challjenkNew -d -p 65000:8000 challengejenkins'  
                                 					
				}                 
			}                  
			stage('Deploy') {                         
				steps {                                 
					echo 'Deploying....'  
					input 'Accept deployment?'
					//sh 'docker stop $(docker ps -aq)'
					sh 'docker stop challjenk challjenkNew'
					sh 'docker rm challjenk'
					//sh 'docker rename challjenk challjenk'
					//sh 'docker rm challjenkNew'
					sh 'docker run --name challjenk -d -p 8000:8000 challengejenkins'  
                                 					
				}                 
			}         
		} 
} 
