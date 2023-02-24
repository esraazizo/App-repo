
pipeline {
    agent { label 'slave-label' }
    stages {
        stage('build') {
            steps {
            	withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh   """
                        docker login -u $USERNAME -p $PASSWORD
                        docker build -t esraazoz/hello-world ./app/
                        docker push esraazoz/hello-world
                    """
                 }
            }
        }
        stage('deploy') {
            steps {
                    sh    """
                        kubectl apply -f deploy -n app-ns
                    """
            }
        }
    }
}
