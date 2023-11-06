pipeline{
    agent any
    stages{

        stage("getting code") {
            steps {
                git url: 'https://github.com/mohamedsadokmasghouni/tp3-app', branch: 'main',
                // credentialsId: 'github-credentials' //jenkins-github-creds
                sh "ls -ltr"
            }
        }

        stage('build and push docker image')
                {
              steps{
                  script{
                    sh 'docker build -t sadook/tp3:latest .'
		            withCredentials([string(credentialsId: 'docker-password', variable: 'docker-password')]) {
                        sh 'docker login -u sadook -p $docker-password'
                        sh 'docker push sadook/tp3:latest'
                    }
                  }
              }
        }
    }
}
