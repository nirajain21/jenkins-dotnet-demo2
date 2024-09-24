pipeline {
    agent any

    stages {
        stage('Restore') {
            steps {
                echo 'Restoring dependencies...'
                sh '/bin/sh -c "/usr/local/share/dotnet/dotnet restore Jenkins.sln"'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh '/bin/sh -c "/usr/local/share/dotnet/dotnet build Jenkins -c Release --no-restore"'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh '/bin/sh -c "/usr/local/share/dotnet/dotnet test Jenkins --no-build --verbosity normal"'
            }
        }

        stage('Publish') {
            steps {
                echo 'Publishing the project...'
                sh '/bin/sh -c "/usr/local/share/dotnet/dotnet publish Jenkins.sln -c Release -o ./publish"'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            cleanWs()
        }
    }
}
