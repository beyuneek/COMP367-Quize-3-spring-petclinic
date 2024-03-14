pipeline {
    agent any

    triggers {
        cron('H/10 * * * 4')
    }

    stages {
        stage('Build') {
            steps {
                script {
                    
                    bat 'mvn clean package'
                }
            }
        }
        stage('Generate JaCoCo Report') {
            steps {
                script {
                    
                    bat 'mvn test jacoco:report'
                }
            }
        }
    }
}