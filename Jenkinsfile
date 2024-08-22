pipeline {
    agent {
        node { 
            label 'any'
            checkout scm
            def pom = readMavenPom file: 'pom.xml'
        }   
    }
    stages {
        stage('Checkout') {
            steps {
                    echo "pom - ${pom}"
                    echo "pom.name - ${pom.name}"
                    echo "pom.version ${pom.version}"
            }
        }
        
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
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
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
