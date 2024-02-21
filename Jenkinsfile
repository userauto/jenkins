pipeline {
    agent any

    stages{
        stage('Github pull'){
            steps {
                sh '''
                    cd /var/lib/jenkins/github
                    git clone git@github.com:userauto/jenkins.git
                '''
            }
        }
    } 
}
