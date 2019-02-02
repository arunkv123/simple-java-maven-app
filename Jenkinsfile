pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2 -w /C/Users/arun/.jenkins/workspace/Docker_test_master -v /C/Users/arun/.jenkins/workspace/Docker_test_master:/C/Users/arun/.jenkins/workspace/Docker_test_master:rw -v /C/Users/arun/.jenkins/workspace/Docker_test_master@tmp:/C/Users/arun/.jenkins/workspace/Docker_test_master@tmp:rw'
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
