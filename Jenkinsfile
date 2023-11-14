pipeline {
    agent any
        stages {
            stage ('Checkout') {
                steps {
                    git branch:'master', url: 'https://github.com/OWASP/Vulnerable-Web-Application.git'
                    }
                    }
                    stage('Code Quality Check via SonarQube') {
                    steps {
                    script {
                    def scannerHome = tool 'SonarQube';
                    withSonarQubeEnv('SonarQube') {
                    sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP - Dsonar.sources=sqp_a7189f0c054eb1ba53f1140f15f6df3d94c49a4a"
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


