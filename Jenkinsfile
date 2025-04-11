pipeline {
    agent any

    tools {
        // Install the Maven version configured as "maven-398" and add it to the path.
        maven "maven-398"
    }

    stages {
        stage('Check Maven') {
            steps {
                sh "if ! command -v mvn; then echo 'Maven not found!'; exit 1; fi"
            }
        }

        stage('Build') {
            steps {
                git branch: 'main', url: 'http://localhost:5555/dasher-org/jenkins-hello-world.git'
                sh "mvn clean package -DskipTests=true"
            }
        }

        stage('Integration Testing') {
            steps {
                sh "sleep ${params.SLEEP_TIMER}"
                sh """ curl -s http://localhost:${params.APPLICATION_PORT}/hello | grep -i "Hello, KodeKloud community!" """
            }
        }   
    }
}