pipeline{
    agent any
    
    tools{
        jdk 'java-11'
        maven 'maven'
    }
    
    stages{
        stage('Git-checkout'){
            steps{
                git branch: 'master' , url: 'https://github.com/VinayGowdru-cloud/web-application.git'
            }
        }
        stage('Code Compile'){
            steps{
                sh 'mvn compile'
            }
        }
        stage('Code Package'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('Build and tag'){
            steps{
                sh 'docker build -t vinay24102002/puneetrajkumar3 .'
            }
        }
        stage('Containerisation'){
            steps{
                sh '''
                docker run -it -d --name c4 -p 9004:8080 vinay24102002/puneetrajkumar3 
                '''
            }
        }
        stage('Login to Docker Hub') {
                    steps {
                        script {
                            withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                                sh "echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin"
                            } 
                        }
                    }  
        }       
        
         stage('Pushing image to repository'){
            steps{
                sh 'Docker Hub push vinay24102002/puneetrajkumar3'
            }
        }
        
    }
}
