pipeline {
    agent any

    stages{
        stage('Github clone') {
            steps {
                sh '''
                    rm -rf jenkins /var/lib/jenkins/github
                    git clone git@github.com:userauto/jenkins.git /var/lib/jenkins/github
                    cd /var/lib/jenkins/github
                    pwd
                '''
            }
        }
        stage('Run docker Nginx') {
            steps {
                sh '''
                    /* groovylint-disable-next-line LineLength */
                    docker run --name nginx --rm -u root -d -p 9889:80 -v /var/lib/jenkins/github/site:/var/www/html nginx:latest
                '''
            }
        }
        stage('Check code reply HTTP') {
            steps {
                sh '''
                    curl -I http://158.160.67.74:9889/ 2>/dev/null | head -n 1 | cut -d$' ' -f2
                '''
            }
        }
    } 
}