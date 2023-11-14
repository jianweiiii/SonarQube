pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/OWASP/Vulnerable-Web-Application.git'
            }
        }
        stage('Code Quality Check via SonarQube') {
            steps {
                script {
                    def scannerHome = tool 'SonarQube'
                    withSonarQubeEnv('SonarQube') {
                        sh "${scannerHome}/bin/sonar-scanner -X -Dsonar.projectKey=OWASP -Dsonar.sources=. -Dsonar.host.url=http://192.168.50.44:9000 -Dsonar.login=sqp_a7189f0c054eb1ba53f1140f15f6df3d94c49a4a"
                    }
                }
            }
        }
    }
    post {
        always {
            recordIssues enabledForFailure: true, tools: [sonarQube()]
        }
    }
}