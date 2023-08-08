pipeline {
    agent any
    
    stages {
        stage('Clone Repository') {
            steps {
                // Clean workspace before cloning
                deleteDir()
                
                // Clone the GitHub repository
                checkout([$class: 'GitSCM',
                          branches: [[name: 'simple-reactjs']], // Specify the branch you want to build
                          userRemoteConfigs: [[url: 'https://github.com/VISHNU-KUMAR7/ReactJs_Devops_K8s.git']]])
            }
        }

        stage('Build Docker Image') {
            agent {
                label 'node1'
            }
            steps {
                script {
                    // Define variables
                    def imageName = 'my-reactjs-image'
                    def dockerfilePath = 'Dockerfile' // Path to your Dockerfile

                    // Build the Docker image
                    sh 'sudo docker build -t my-react-app .'
                }
            }
        }
        
        // stage('Build Docker Image') {
        //     steps {
        //         // Build the Docker image
        //         script {
        //             def imageName = "my-docker-image"
        //             def imageTag = env.BUILD_NUMBER
                    
        //             docker.build("${imageName}:${imageTag}", ".")
        //         }
        //     }
        // }
        
        // stage('Push Docker Image') {
        //     steps {
        //         // Push the Docker image to a registry
        //         script {
        //             def imageName = "my-docker-image"
        //             def imageTag = env.BUILD_NUMBER
        //             def registryUrl = "docker.registry.com"
                    
        //             docker.withRegistry("${registryUrl}", 'docker-credentials') {
        //                 docker.image("${imageName}:${imageTag}").push()
        //             }
        //         }
        //     }
        // }
    }
    
    // post {
    //     always {
    //         // Clean up steps or notifications
    //     }
    //     success {
    //         // Actions to perform on success
    //     }
    //     failure {
    //         // Actions to perform on failure
    //     }
    // }
}
