pipeline { 
    environment { 
        registry = "lalithyvlk/nodejs-app" 
        registryCredential = 'dockerhub' 
        dockerImage = '' 
    }
    agent any 
    stages { 
        stage('Cloning our Git') { 

            steps { 

                git 'https://gitlab.presidio.com/lalith-runner-grp/lalith-nodejs-jenkins' 

            }

        } 
        stage('Building our image') { 
            steps { 
                script { 
                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 
                }
            } 
        }
        stage('Deploy our image') { 
            steps { 
                script { 
                    docker.withRegistry( '', registryCredential ) { 
                        dockerImage.push() 
                    }
                } 
            }
        } 
        stage('Cleaning up') { 
            steps { 
                sh "docker rmi $registry:$BUILD_NUMBER" 
            }
        } 
    }
}


