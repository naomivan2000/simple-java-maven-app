pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
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
        stage('Delivery') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
        stage('Archive_Package') {
            steps {
                archiveArtifacts artifacts: 'target/my-app-1.0-SNAPSHOT.jar, target/surefire-reports/*', followSymlinks: false
            }
        }
    }
}

