pipeline {
    agent any
    tools {
        maven 'Maven3'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Code Coverage') {
            steps {
                sh 'mvn org.jacoco:jacoco-maven-plugin:prepare-agent test org.jacoco:jacoco-maven-plugin:report'
            }
            post {
                always {
                    jacoco(execPattern: '**/*/target/site/jacoco/jacoco.xml')
                }
            }
        }
    }
    triggers {
        cron('H/10 * * * 4')
    }
}
