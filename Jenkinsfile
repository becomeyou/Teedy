pipeline {
    agent any
    stages {
        stage('Package') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [],
                userRemoteConfigs: [[url: 'https://github.com/becomeyou/Teedy.git']])
                sh 'mvn -B -DskipTests clean package'
            }
        }
          stage('Building image') {
            steps {
                sh 'sudo docker build -t teedy2024_manual .'
            }
        }
        stage('Upload image') {
            
            steps {     
            
                
                sh 'sudo docker login -u youbecome -p lu3445535'
               
                       sh 'sudo docker tag teedy2024_manual youbecome/teedytry1:v1.0'
                       sh 'sudo docker push youbecome/teedytry1:v1.0'
                    
                
            }
        }
        stage('Run containers') {
            steps {
                sh 'sudo docker run -d -p 8084:8080 --name teedy_manual01 youbecome/teedytry1:v1.0'
                sh 'sudo docker run -d -p 8082:8080 --name teedy_manual02 youbecome/teedytry1:v1.0'
                sh 'sudo docker run -d -p 8083:8080 --name teedy_manual03 youbecome/teedytry1:v1.0'
            }
        }
    }
}
