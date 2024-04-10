pipeline {
    agent any

    environment {
        DOCKER_HUB_PASSWORD = credentials('docker_pass')
    }

    stages {
        stage("getting code") {
            steps {
                git url: 'https://github.com/mouralisandra/Tp3Kubernetes.git', branch: 'main',
                credentialsId: 'github-credentials' 
            }
        }
      
        stage("Build Docker Image") {
            steps {
                script {
                 sh "docker build -t devopstp:v1 ."

                    
                }
            }
        }

        stage("Push to Docker Hub") {
            steps {
                script {
                    echo "======== executing ========"
                    echo "push to hub"
                         docker.withRegistry('https://registry-1.docker.io/v1/', 'docker_pass') {
                        def dockerImage = docker.image("devopstp:v1")
                        dockerImage.push()
                         }
                }
            }
        }

        stage('Deploying App to Kubernetes') {
            steps {
                script {
                    kubernetesDeploy(configs: "deployment.yml", kubeconfigId: "kubernetes")
                }
            }
        }
    }
}
