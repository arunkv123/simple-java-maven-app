pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v <host_home_path>/.m2:/root/.m2'
            reuseNode true
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }	
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.bat'
            }
        }
    }
}
