/* groovylint-disable LineLength */
pipeline {
    agent any

    stages {
        stage('Pipeline') {
            steps {
                script {
                    stage('Build & Test'){
                        sh "./gradlew clean build"
                    }

                    stage('Sonar'){
                        //corresponde al scanner configurado en global tools Jenkins
                        def scannerHome = tool 'sonar-scanner';
                        //corresponde a lo configurado en sistema Jenkins
                        withSonarQubeEnv('sonar-server') { 
                            bat "${scannerHome}\\bin\\sonar-scanner -Dsonar.projectKey=ejemplo-gradle -Dsonar.java.binaries=build"
                        }
                    }

                    stage('Run') {
                        sh 'gradlew bootRun &'
                        sh 'sleep 20'
                    }
                    stage('Rest') {
                        sh 'curl -X GET "http://localhost:8888/rest/mscovid/test?msg=testing"'
                    }

                    stage('Nexus'){
                        nexusPublisher nexusInstanceId: 'nexus', nexusRepositoryId: 'test-repo', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: 'jar', filePath: 'C:/Proyectos/ejemplo-gradle/build/libs/DevOpsUsach2020-0.0.1.jar']], mavenCoordinate: [artifactId: 'DevOpsUsach2020', groupId: 'com.devopsusach2020', packaging: 'jar', version: '0.0.1']]]
                    }
                }
            }
        }
    }
}
