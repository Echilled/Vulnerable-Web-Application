pipeline {
    agent any
 options {
        // This is required if you want to clean before build
        skipDefaultCheckout(true)
    }
    stages {
        stage('Clean Workspace before build') {
            steps {
                // Clean before build
                cleanWs()
            }
        }
        stage('Code Quality Check Via SonarQube') {
            steps {
                    script {
                        def scannerHome = tool 'SonarQube';
                        withSonarQubeEnv('SonarQube') {
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=​ OWASP -Dsonar.sources=."
                    }
                }
            }
        }
  stage('OWASP Dependency-Check Vulnerabilities') {
   steps {
    dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
   }
  }
    }
 post {
  success {
   dependencyCheckPublisher pattern: 'dependency-check-report.xml'
  }
 }
}
