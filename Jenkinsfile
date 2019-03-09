pipeline{
    agent {
        docker {
            args '-v /root/.m2:/root/.m2'
            image 'maven:3-alpine'
        }
    }
    stages {
        stage('Build') {
            steps{
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test'){
            steps{
                sh 'mvn test'
            }
            post{
                always{
                    sh 'echo current directory:'
                    sh 'pwd'
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver'){
            steps{
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }

}
