pipeline {
    agent any
    tools {
        maven 'M3' // Make sure this matches the name of the Maven installation in your Jenkins configuration.
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
            // This step requires the Code Coverage API plugin to be installed in Jenkins.
            publishCoverage adapters: [jacocoAdapter('**/target/site/jacoco/jacoco.xml')]
        }
    }
    triggers {
        cron('H/10 * * * 4') // This will trigger the pipeline every 10 minutes on Thursdays.
    }
}
