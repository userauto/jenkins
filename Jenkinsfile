/* groovylint-disable-next-line CompileStatic */
pipeline {
    agent any

    stages {
        stage('Github clone') {
            steps {
                sh 'echo "Repository has cloned"'
            }
        }
        stage('Run docker Nginx') {
            steps {
                /* groovylint-disable-next-line LineLength */
                sh 'docker run --name nginx --rm -d -p 9889:80 -v ./site:/usr/share/nginx/html nginx:latest'
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
        success {
            sh 'curl -X POST -H "Content-Type: application/json" -d \'{"chat_id": "884174870", "text": "[SUCCSESS] build success!", "disable_notification": false}\' https://api.telegram.org/bot7094254109:AAF1KYBKvInh252FPJAaq0gG3EeH1qmnUFI/sendMessage'
        }
        failure {
            sh 'curl -X POST -H "Content-Type: application/json" -d \'{"chat_id": "884174870", "text": "[💀FAILED] Ukata api build failed!", "disable_notification": false}\' https://api.telegram.org/bot7094254109:AAF1KYBKvInh252FPJAaq0gG3EeH1qmnUFI/sendMessage'
        }
    }
}