pipeline {
    environment {
        IMAGE_NAME = "alpinehelloworld-jenkins"
        IMAGE_TAG = "latest"
        STAGING = "mini-projet-jenkins-staging"
        PRODUCTION = "mini-projet-jenkins-production"
    }
    agent none
    stages {
        stage ('Build image'){
            agent any
            steps {
                script {
                    sh 'docker build -t toshiroskynet/$IMAGE_NAME:$IMAGE_TAG .'
                }
            }
        }
        stage ('Run container based on builded image'){
            agent any
            steps {
                script {
                    sh '''
                        docker run --name $IMAGE_NAME -d -p 81:5000 -e PORT=5000 toshiroskynet/$IMAGE_NAME:$IMAGE_TAG
                        sleep 10
                    '''
                }
            }
        }
        stage ('Test image'){
            agent any
            steps {
                script {
                    sh '''
                        curl http://172.17.0.1:81 | grep -i 'Hello World'
                    '''
                }
            }
        }
        stage ('Clean container'){
            agent any
            steps {
                script {
                    sh '''
                        docker stop $IMAGE_NAME
                        docker rm $IMAGE_NAME
                    '''
                }
            }
        }
        stage ('Push image in staging and deploy it'){
            when {
                expression { GIT_BRANCH == 'origin/main' }
            }
            agent any
            environment {
                HEROKU_API_KEY = credentials('heroku_api_key')
            }
            steps {
                script {
                    sh '''
                        npm i -g heroku@7.68.0
                        heroku container:login
                        heroku create $STAGING || echo "project already exist"
                        heroku container:push -a $STAGING web
                        heroku container:release -a $STAGING web
                    '''
                }
            }
        }
        stage ('Push image in production and deploy it'){
            when {
                expression { GIT_BRANCH == 'origin/main' }
            }
            agent any
            environment {
                HEROKU_API_KEY = credentials('heroku_api_key')
            }
            steps {
                script {
                    sh '''
                        npm i -g heroku@7.68.0
                        heroku container:login
                        heroku create $PRODUCTION || echo "project already exist"
                        heroku container:push -a $PRODUCTION web
                        heroku container:release -a $PRODUCTION web
                    '''
                }
            }
        }
    }
    post {
        success {
            slackSend (color: '#00FF00', message: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
        }
        failure {
            slackSend (color: '#FF0000', message: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
        }   
    } 
}