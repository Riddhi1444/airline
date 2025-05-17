pipeline {
    agent {
        docker {
            image 'maven:3.8.5-openjdk-17'
        }
    }

    environment {
        JAR_NAME = 'airline-0.0.1-SNAPSHOT.jar'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/Riddhi1444/airline.git'
            }
        }

        stage('Build Project') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Start Spring Boot App') {
            steps {
                sh '''
                echo "Stopping any existing app..."
                pkill -f $JAR_NAME || true

                echo "Starting the new app..."
                nohup java -jar target/$JAR_NAME > app.log 2>&1 &
                '''
            }
        }
    }

    post {
        success {
            echo 'Build and deployment succeeded!'
        }
        failure {
            echo 'Build failed.'
        }
    }
}
