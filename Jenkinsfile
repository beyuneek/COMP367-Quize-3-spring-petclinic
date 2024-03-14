pipeline {
    agent any
    tools {
        maven 'M3' // Make sure 'M3' is configured in your Global Tool Configuration
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
        }
    }
    post {
        always {
            // Use the publishCoverage step provided by the Code Coverage API plugin, which may need to be installed separately
            publishCoverage adapters: [jacocoAdapter('**/target/site/jacoco/jacoco.xml')]
        }
    }
    triggers {
        cron('H/10 * * * 4') // This triggers the build every 10 minutes on Thursdays
    }
}

