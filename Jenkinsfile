pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/samanthalam18/Vulnerable-Web-Application.git'
            }
        }
        stage('Code Quality Check via SonarQube') {
            steps {
                script {
                    def scannerHome = tool 'SonarQube'
                    withSonarQubeEnv('SonarQube') {
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=. -Dsonar.host.url=http://sonarqube:9000 -Dsonar.token=sqp_78e931c362c152f47d2bdec761dd996943a31ff4"
                    }
                }
            }
        }
    }
    post {
        always {
            recordIssues enabledForFailure: true, tool: sonarQube()
        }
    }
}
