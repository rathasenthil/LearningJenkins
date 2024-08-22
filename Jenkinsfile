pipeline {
    agent node { 
        any 
        def pom = readMavenPom file: 'pom.xml'
        echo " pom - ${pom}"
        echo  "pom.name - ${pom.name}"
        echo  "pom.version ${pom.version}"
    }
    stages {
        
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
