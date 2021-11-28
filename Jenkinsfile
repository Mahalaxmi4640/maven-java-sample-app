pipeline {
    agent any

    stages {
       
        stage('Build') {
            steps {
                echo 'Build'
                bat 'mvn compile'
            }
        }
        stage('test') {
            steps {
                echo 'test'
                bat 'mvn test'
            }
        }
        stage('package') {
            steps {
                echo 'package'
                bat 'mvn package'
            }
            post {
          always {
            junit 'target/surefire-reports/*.xml'
          }
          success{
              archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
          }
        }

        }
        stage('Deploy') {
            steps {
                withEnv(['JENKINS_NODE_COOCKIE=dontkillme']){
                echo 'Deploy'
                bat ' java -jar -Dserver.port=8001 target/spring-petclinic-2.3.1.BUILD-SNAPSHOT.jar '
                }
            }
        }
    }
}

