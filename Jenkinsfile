pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo '🔨 Building the project...'
                sh 'mvn clean install -Dmaven.test.skip=true'
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running tests...'
                sh 'mvn surefire-report:report'
                echo '✅ Test completed.'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube-scanner') {
                    echo '🔍 Running SonarQube analysis with Maven...'
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }

    post {
        success {
            echo '🎉 Pipeline completed successfully!'
        }
        failure {
            echo '❌ Pipeline failed.'
        }
    }
}

