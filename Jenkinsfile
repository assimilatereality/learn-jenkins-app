pipeline {
    agent any

    stages {
        /* This is a comment
        line 1
        line2
        */
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'Test stage'
                sh '''
                    test -f build/index.html
                    npm test
                '''
            }
        }
    }

    post {
        always {
            sh 'pwd'
            sh 'ls -la'
            sh 'find . -name "junit.xml"'
            junit 'test-results/junit.xml'
        }
    }
}