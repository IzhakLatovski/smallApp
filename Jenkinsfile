pipeline {
    agent any

    stages {
        stage('First') {
            steps {
                echo '!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!'
            }
        }
        
        stage('Pull') {
            steps {
                sh 'rm -r *'
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                echo '=========================================== Building ==========================================='
                sh 'docker build -t portfolio-small_app-image .'
                script {
                    dockerImage = docker.build "046432083464.dkr.ecr.eu-west-2.amazonaws.com/portfolio" + ":$BUILD_NUMBER"
                }
            }
        }

        stage('Test') {
            steps {
                echo '=========================================== Testing ==========================================='
                // sh 'docker-compose up --build -d'
                // sh 'sleep 20'
                // sh 'curl myip:port'
                // sh 'docker-compose down'
            }
        }

        // Tag the dockerImage

        stage('Deploy') {
            steps {
                echo '=========================================== Deploying ==========================================='
                script{
                docker.withRegistry("https://" + "046432083464.dkr.ecr.eu-west-2.amazonaws.com/portfolio", "ecr:eu-west-2:" + "portfoliocredentials") {
                    dockerImage.push()
                }
            }
            }
        }

    }

    // post {
    //     always {
    //         sh 'docker-compose down'
    //     }
    // }
}
