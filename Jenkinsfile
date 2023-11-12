pipeline {
  agent any
  stages {
  stage('Git Checkout') {
            steps {
                script {
                    git branch: 'JenkinsDependencyCheckTest.git',
                        credentialsId: '3103labs',
                        url: 'https://github.com/raymousray/JenkinsDependencyCheckTest.git'
                }
            }
        }
    stage('OWASP DependencyCheck') {
      steps {
        script {
          // Run OWASP DependencyCheck with additional arguments
          dependencyCheck additionalArguments: " -o './' -s './' -f 'ALL'--format HTML --format JSON", odcInstallation: 'ODC'
        }
      }
    }
  }

  post {
    always {
      // Add post-build action to analyze DependencyCheck reports using the Warnings Next Generation Plugin
      recordIssues enabledForFailure: true, tool: owaspDependencyCheck(pattern: 'dependency-check-report.json')
    }
  }
}
