pipeline {
    agent any 
    tools {
        gradle 'gradlejenkins'
        maven 'mavenjenkins'
    }
    stages {
        stage('Build & Test') { 
            steps {
                sh 'gradle build'
            }
        }
        stage('Sonar') { 
            steps {
                withSonarQubeEnv('SonarQB')  {
                    -Dsonar.projectKey=ejemplo-gradle -Dsonar.java.binaries=build
                }
            }
        }
        stage('Run') { 
            steps {
                sh 'gradle bootRun' 
            }
        }
        stage('Test') {
            steps {
                curl -X GET 'http://localhost:8081/rest/mscovid/test?msg=testing'
            }
        }
        stage ('Nexus') {
            steps {
                 nexusPublisher nexusInstanceId: 'nexus01', nexusRepositoryId: 'devops-usach-nexus', packages: []               
            }
        }
       }
}