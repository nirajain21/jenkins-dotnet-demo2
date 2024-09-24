pipeline {
    agent any

    stages {
        stage('Restore') {
            steps {
                echo 'Restoring dependencies...'
                sh '/bin/sh -c "/usr/local/share/dotnet/dotnet restore TASK 6.2HD.sln"'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh '/bin/sh -c "/usr/local/share/dotnet/dotnet build TASK 6.2HD.sln -c Release --no-restore"'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh '/bin/sh -c "/usr/local/share/dotnet/dotnet test TASK 6.2HD.sln --no-build --verbosity normal"'
            }
        }

        stage('Publish') {
            steps {
                echo 'Publishing the project...'
                sh '/bin/sh -c "/usr/local/share/dotnet/dotnet publish TASK 6.2HD.sln -c Release -o ./publish"'
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
