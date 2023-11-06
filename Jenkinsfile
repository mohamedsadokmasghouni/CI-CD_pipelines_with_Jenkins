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
                    sh 'sudo -S docker build -t sadook/tp3:latest .'
		            withCredentials([string(credentialsId: 'docker-password', variable: 'docker-password')]) {
                        sh 'sudo docker login -u sadook -p $docker-password'
                        sh 'sudo docker push sadook/tp3:latest'
                    }
                  }
              }
        }
    }
}
