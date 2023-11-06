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
