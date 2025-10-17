pipeline{
    agent any
    environment{
        DOCKER_IMG='babugudageri/continues-intigration:1'
    }
    tools{
        jdk 'java-11'
        maven 'maven'
    }
    stages{
        stage('Git Checkout'){
            steps{
                 git branch:'master', url: 'https://github.com/BasavarajGudageri-05/jenkinsdeployment.git' 
            }
        }
        stage('compile'){
            steps{
            sh 'mvn compile'
            }
        }
        stage('clean'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('docker build'){
            steps{
                sh 'docker build -t $DOCKER_IMG .'
            }
        }
        stage('containerasation'){
            steps{
                sh '''
                docker stop c1 || true
                docker rm c1 || true
                docker run -it -d --name c1 -p 9000:8080 $DOCKER_IMG 
                '''
            }
        }
        stage('docker login'){
            steps{
                script{
                    withCredentials([usernamePassword(credentialsId: 'Docker', passwordVariable: 'DOCKER-PASSWORD', usernameVariable: 'DOCKER-USERNAME')]) 
                {
                    sh " echo $DOCKER-PASSWORD | docker login -u DOCKER-USERNAME --password-stdin"
                }

             
                }
            }
        }
        stage('push image to docker hub'){
            steps{
                sh "docker push $DOCKER_IMG"
            }
        }
    }
    
}
