pipeline {
    agent any
    tools {
        maven 'Maven'
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
                    echo "building the docker image..."
                    withCredentials([usernamePassword(credentialsId:'docker', passwordVariable:'PASS', usernameVariable: 'USER')]){
                        sh 'docker build -t chimenco/java-mvn:v1 .'
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh 'docker push chimenco/java-mvn:v1'
                    }
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    echo "deploying the application"
                }
            }
        }
    } 
}
