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

                    stage('Run'){
                        //
                    }

                    stage('Rest'){
                        //
                    }

                    stage('Nexus'){
                        //
                    }
                }
            }
        }
    }
}
