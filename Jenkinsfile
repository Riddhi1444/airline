pipeline {
    agent {
        docker {
            image 'maven:3.8.5-openjdk-17'
        }
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/Riddhi1444/airline.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Start Locally') {
            steps {
                sh '''
                pkill -f target/airline-0.0.1-SNAPSHOT.jar || true
                nohup java -jar target/airline-0.0.1-SNAPSHOT.jar > app.log 2>&1 &
                '''
            }
        }
    }
}
