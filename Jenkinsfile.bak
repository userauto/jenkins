/* groovylint-disable-next-line CompileStatic */
pipeline {
    agent any

    stages {
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
                /* groovylint-disable-next-line LineLength */
                sh 'docker run --name nginx --rm -d -p 9889:80 -v /var/lib/jenkins/github/site:/usr/share/nginx/html nginx:latest'
            }
        }
        stage('Check code reply HTTP') {
            steps {
                sh 'sleep 10'
                sh 'curl -s -o /dev/null -w "%{http_code}" http://158.160.67.74:9889/'
            }
        }
        stage('Check md5') {
            steps {
                sh '''
                    echo "Hash sum file index.html"
                    md5sum /var/lib/jenkins/github/site/index.html | awk '{print$1}'
                    echo "Hash sum reply HTTP"
                    curl http://158.160.67.74:9889/ 2> /dev/null | md5sum | awk '{print$1}'
                '''
            }
        }
        stage('Stop docker nginx') {
            steps {
                sh 'docker stop nginx'
            }
        }
    }
    post {
        always {
            mail to: 'aleksey.potapov@bk.ru',
            subject: 'Test Email',
            body: 'Test'
        }
    }
}