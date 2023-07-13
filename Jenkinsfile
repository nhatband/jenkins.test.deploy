Jenkinsfile (Declarative Pipeline)
/* Requires the Docker Pipeline plugin */
pipeline {
    agent { docker { image 'mcr.microsoft.com/dotnet/samples:aspnetapp' } }
    stages {
        stage('build') {
            steps {
                sh 'dotnet --version'
            }
        }
    }
}