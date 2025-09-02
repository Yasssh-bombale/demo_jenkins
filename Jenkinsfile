pipeline {
    agent any

    stages {
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
        stage('Deploy') {
            agent {
              docker {
                image 'node:18-alpine'
                reuseNode true
              } 
            }
            steps {
                sh '''
                    npm install netlify-cli@20.1.1
                    node_modules/.bin/netlify --version
                '''
            }
        }
    }
}
