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
stage('Docker Build and Deploy') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t dotnet-app-image .' // Build the Docker image from the Dockerfile

                echo 'Running Docker container...'
                sh 'docker stop dotnet-app-container || true && docker rm dotnet-app-container || true' // Stop and remove any existing container with the same name
                sh 'docker run -d -p 8080:80 --name dotnet-app-container dotnet-app-image' // Run the container, mapping port 8080 on the host to port 80 on the container
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
