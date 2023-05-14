pipeline {
    agent any 
    environment {
        PATH = "$PATH:/usr/local/bin"
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
        stage('Check Path') {
            steps {
                sh 'echo $PATH'
            }
        }
        stage("build image") {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-login', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    script {
                        echo "building the docker image"
                        sh "docker build -t bukkysven/jenkins-test:demo-apache ."
                        sh "echo \$PASS | docker login -u \$USER --password-stdin"
                        sh "docker push bukkysven/jenkins-test:demo-apache"
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
