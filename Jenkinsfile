pipeline {
    agent any 
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
        stage('Check Path') {
            steps {
                sh 'echo $PATH'
            }
        }
        stage("build image") {
            steps {
                script {
                    echo "building the docker image"
                    withCredentials([usernamePassword(credentialsId: 'docker-login', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh 'docker build -t bukkysven/jenkins-test:demo-apache .'
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh 'docker push bukkysven/jenkins-test:demo-apache' 
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
