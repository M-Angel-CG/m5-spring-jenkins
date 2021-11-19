pipeline {
    agent any
    tools {
        maven "maven3.8.3"
        jdk "jdk17-nuevo"
    }
    stages {
        stage("Env Variables") {
            steps {
                sh "printenv"
            }
        }
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
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
        stage('Site') {
            steps {
                sh 'mvn site'
            }
        }
        stage('Sonar'){
            steps {
                sh 'mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=m5spring-jenkins -Dsonar.login=25ea7b9bae1de44d60a43b073ee519600bbf8994 -Dsonar.host.url=https://sonarcloud.io -Dsonar.organization=m-angel-cg'
            }
        }

    }
}
