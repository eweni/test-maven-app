pipeline {
    agent any
    environment {
    PATH = "$PATH:/usr/local/bin/docker"
}

    tools {
        maven 'maven-3.9'
    }
    stages {
        
        stage("build jar") {
            steps {
                script {
                    echo "building the application"
                    sh 'mvn package'
                }
            }
        }
        stage("build image") {
            steps {
                script {
                    try {
                        withCredentials([usernamePassword(credentialsId: 'docker-login', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                            sh 'docker build -t bukkysven/jenkins-test:demo-apache .'
                            sh 'docker run --rm bukkysven/jenkins-test:demo-apache echo "Docker build successful"'
                            sh "echo $PASS | docker login -u $USER --password-stdin"
                            sh 'docker push bukkysven/jenkins-test:demo-apache'
                        }
                    } catch (err) {
                        currentBuild.result = 'FAILURE'
                        error "Failed to build or push Docker image: ${err}"
                    } 
                    
                        
                    
                }
            }


        } 
        stage("deploy") {
            steps {
                script {
                    echo "deploying"
                    
                }
            }
        }
    }   
}
