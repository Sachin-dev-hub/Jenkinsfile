pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo '🔨 Building the project...'
                sh 'mvn clean deploy -Dmaven.test.skip=true'
            }
        }
    
        stage('Test') {
            steps {
				echo 'test starting'
                sh 'surefire-report:report'
				echo 'test completed'
            }
        }

    
        stage('SonarQube Analysis') {
			environment {
				scannerHome = tool 'sonarqube-scanner'
			}
				
            steps {
                withSonarQubeEnv('sonarqube-scanner') {
                    sh "${scannerHome}/bin/sonar-scanner"
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










