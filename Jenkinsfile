pipeline {

    agent any
    
    environment {
        // Give Image Name as per your choice
        imageRepository = "myrepo"
        // Give ACR login Server Name
        loginServer = "myregistry.azurecr.io"
        // Add ACR credentials in Jenkins credentials and provide it's ID here
        registryCredential = "myACRCredentials"
        dockerImage = ""
    }
    
    stages {
        
        // Checkout Github Repository
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/samyakj01/PaaS-Migrator']]])
            }
        }
        
        // Building Docker Image
        stage('Build Docker Image') {
            steps {
                dir('BookListMVC') {
                    script {
                        dockerImage = docker.build imageRepository
                    }
                }
            }
        }
        
        // Uploading Docker Images to ACR
        stage('Upload Image to ACR') {
            steps {   
                script {
                    docker.withRegistry( "http://$loginServer", registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
        
        // Stopping Previous Running container
        stage('stop Previous Containers') {
            steps {
               bat "docker rm -f mywebapp"
               bat "docker ps -a"
            }
        }
       
        // Running Fresh Container
        stage('Docker Run') {
            steps {
                script {
                   bat "docker run -d -p 8090:80 --rm --name myPOCwebapp $loginServer/$imageRepository"
                }
            }
       }
    }
}