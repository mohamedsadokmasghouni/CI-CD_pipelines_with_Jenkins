pipeline{
    agent any
    stages{

        stage("getting code") {
            steps {
                git url: 'https://github.com/mohamedsadokmasghouni/tp3-app', branch: 'main',
                credentialsId: 'github-credentials' //jenkins-github-creds
                sh "ls -ltr"
            }
        }

        stage('build and push docker image')
                {
              steps{
                  script{
                    sh 'docker build -t sadook/tp3:latest .'
		        withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
                        sh 'docker login -u ${DOCKER_USER} -p ${DOCKER_PASS}'
                        sh 'docker push sadook/tp3:latest'
                    }
                  }
              }
        }
    }
}
