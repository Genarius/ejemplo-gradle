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
                    //sh '-Dsonar.projectKey=ejemplo-gradle -Dsonar.java.binaries=build'
                    echo 'Probando el stage Sonar'
                }
            }
        }
        stage('Run') { 
            steps {
                // sh 'gradle bootRun' 
                echo 'Stage RUN'
            }
        }
        stage('Test') {
            steps {
                // sh 'curl -X GET http://localhost:8081/rest/mscovid/test?msg=testing'
                echo 'stage TEST'
            }
        }
        stage ('Nexus') {
            steps {
               // nexusPublisher nexusInstanceId: 'nexus01', nexusRepositoryId: 'devops-usach-nexus', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '/build/DevOpsUsach2020-0.0.2.jar']], mavenCoordinate: [artifactId: 'DevOpsUsach2020', groupId: 'com.devopsusach2020', packaging: 'jar', version: '0.0.2']]]
               echo 'Stage Nexus'
            }
        }
       }
}