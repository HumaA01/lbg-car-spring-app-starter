pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
    }

    stages {
        stage('SSH to Server 2'){
            steps{
                script{
                    sshagent(['~/.ssh/id_rsa']){
                        sh 'ssh -t -o StrictHostKeyChecking=no huma_ahmed@livelaughlloyds-docker "echo hello"' 
                    }
                }
            }
            
        }
        stage('Checkout') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', url:'https://github.com/HumaA01/lbg-car-react-starter'
                git branch: 'main', url:'https://github.com/HumaA01/lbg-car-spring-app-starter'

            }
        }
        stage('Compile'){
            steps{
                sh "mvn clean compile"
            }
        }
        stage('Test'){
            steps{
                sh "mvn test"
            }
        }
        stage('Package'){
            steps{
                sh "mvn package"
            }
        }
    }
}
