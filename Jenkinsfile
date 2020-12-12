/* groovylint-disable LineLength */
pipeline {
    agent any

    stages {
        stage('Compile') {
            steps {
                sh 'mvn clean compile -e'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn clean test -e'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn clean package -e'
            }
        }
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv(installationName: 'sonar') {
                    sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
                }
            }
        }
        stage('UploadNexus') {
            steps {
                /* groovylint-disable-next-line DuplicateStringLiteral */
                nexusPublisher nexusInstanceId: 'nexus', nexusRepositoryId: 'test-repo', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: 'jar', filePath: 'C:/Proyectos/ejemplo-maven/build/DevOpsUsach2020-0.0.1.jar']], mavenCoordinate: [artifactId: 'DevOpsUsach2020', groupId: 'com.devopsusach2020', packaging: 'jar', version: '0.0.1']]]
            }
        }
    }
}
