pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
    }

    stages {
        stage('Build') {
            steps {
            
                git branch: 'main', url: 'https://github.com/qf-dhl/core.git'
                 withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {

                sh "mvn -Dmaven.test.failure.ignore=true -s settings.xml clean deploy org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=qf-dhl_core"
                 }
            }

            post {
                
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
