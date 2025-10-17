pipeline{
    agent any
    environment{
        DOCKER_IMG='babugudageri/continues-intigration:1'
    }
    tools{
        jdk 'jdk-11'
        maven 'maven'
    }
    stages{
        stage('Git Checkout'){
            steps{
                url: 'https://github.com/BasavarajGudageri-05/jenkinsdeployment.git', git branch: 'master'
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
                sh 'docker build -t $DOCKER_IMG'
            }
        }
        stage('containerasation'){
            steps{
                sh '''
                docker stop c1 || true
                docker rm c1 || true
                docker run -it -d -p 9000:8080 $DOCKER_IMG --name c1
                '''
            }
        }
    }
    
}
