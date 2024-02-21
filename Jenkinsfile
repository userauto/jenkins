pipeline {
    agent any

    stages{
        stage('Github pull'){
            steps {
                sh '''
                    cd /var/lib/jenkins/github/jenkins
                    git pull git@github.com:userauto/jenkins.git
                '''
            }
        }
    } 
}
