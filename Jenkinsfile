pipeline {
    agent any

    stages{
        stage('Github pull') {
            steps {
                sh '''
                    rm -rf jenkins /var/lib/jenkins/github
                    git clone git@github.com:userauto/jenkins.git /var/lib/jenkins/github
                    cd /var/lib/jenkins/github
                    pwd
                '''
            }
        }
    } 
}