pipeline {
    agent any
    environment {
        NETLIFY_SITE_ID = '42ad2abd-901a-429e-b7b9-73251980938d'
        NETLIFY_AUTH_TOKEN = credentials('netlify-id')
    }
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
                    echo "Deploying to production Site ID: $NETLIFY_SITE_ID"
                    node_modules/.bin/netlify status
                '''
            }
        }
    }
}
