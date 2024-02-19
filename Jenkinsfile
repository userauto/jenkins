/* groovylint-disable-next-line CompileStatic */
pipeline {
    agent any

    stages {
        stage('1-string') {
            steps {
                sh '''
                    /var/lib/jenkins/scripts/print-first-line.sh
                    cat output.sql-1
                '''
            }
        }
        stage('All-RNK-spints') {
            steps {
                sh '''
                    /var/lib/jenkins/scripts/all-rnk-splints.sh
                    cat output.sql-2
                '''
            }
        }
    }
}
