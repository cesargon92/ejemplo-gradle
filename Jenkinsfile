/* groovylint-disable LineLength */
pipeline {
    agent any
    parameters { choice(name: 'selector', choices: ['gradle', 'maven'], description: 'Seleccione') }
    stages {
        stage('Pipeline') {
            steps {
                script {
                    if(params.selector == 'gradle'){
                        def ejecucion = load 'gradle.groovy'
                        ejecucion.call()
                    } else {
                        def ejecucion = load 'maven.groovy'
                        ejecucion.call()
                    }
                }
            }
        }
    }
}
