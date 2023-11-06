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

	stage('Deploy the application on kubernetes cluster')
                {
              steps{
                  script{
                    withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'k8s', namespace: '', restrictKubeConfigAccess: false, serverUrl: '') {
			//sh 'kubectl delete -f k8s/deployment.yaml'
			//sh 'kubectl delete -f k8s/service.yaml'
                        //sh 'kubectl apply -f k8s/deployment.yaml'
			//sh 'kubectl apply -f k8s/service.yaml'
			ansiblePlaybook become: true, installation: 'ansible', inventory: 'localhost', playbook: 'k8s/ansible-playbook.yaml', vaultTmpPath: ''
                    }
                    }
                  }
        }
    }
}
