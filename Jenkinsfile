pipeline{
    agent any
    stages{

        stage("getting code") {
            steps {
                sh "ls"
            }
        }

        stage('build and push docker image')
                {
              steps{
                  script{
                    sh 'echo "Sadok1234567" | sudo -S docker build -t sadook/tp3:latest .'
		            withCredentials([string(credentialsId: 'docker-password', variable: 'docker-password')]) {
                        sh 'echo "Sadok1234567" | sudo -S docker login -u sadook -p $docker-password'
                        sh 'echo "Sadok1234567" | sudo -S docker push sadook/tp3:latest'
                    }
                  }
              }
        }
    }
}
