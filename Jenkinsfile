pipeline{
    agent any
    environment {
        VERSION="${V3}"
    }
  
    stages{
        stage('CLONE REPO') {
          steps {
              sh 'rm -rf dockertest1'
              sh 'git clone https://github.com/rakeshhh4/dockertest1.git'
          }
        }
        
        stage('BUILD DOCKER IMAGE') {
          steps {
                sh 'cd /var/lib/jenkins/workspace/pipeline1/dockertest1'
                sh 'cp /var/lib/jenkins/workspace/pipeline1/dockertest1/* /var/lib/jenkins/workspace/pipeline1'
                sh 'docker build -t rakesh2404/pipelinetest:${VERSION} .'
            }
        }
        stage('PUSH IMAGE TO DOCKER-HUB') {
            steps {
                sh 'docker push rakesh2404/pipelinetest:${VERSION}'
            }
        }
        stage('DEPLOY TO DOCKER HOST') {
            steps {
                sh 'docker -H tcp://172.31.81.249:2375 stop MYAPP '
                sh 'docker -H tcp://172.31.81.249:2375 run --rm -itd --name MYAPP --hostname MYAPP -p 8000:80 rakesh2404/pipelinetest:${VERSION}'
            }
                
        }
        stage('CHECK WEBAPP RECHABILITY') {
            steps {
                sh 'sleep 10s'
                sh 'curl http://3.84.95.201:8000'
            }
        }
    }
}
