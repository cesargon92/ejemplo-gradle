/* groovylint-disable LineLength */
pipeline {
    agent any
    parameters { choice(name: 'selector', choices: ['gradle', 'maven'], description: 'Seleccione') }
    stages {
        stage('Pipeline') {
            steps {
                script {
                    env.TASK = ''
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

    post{
        success {
            def mensaje = "[César González][${env.JOB_NAME}][${params.selector}] Ejecución exitosa"
            slackSend color: 'good', message: mensaje, tokenCredentialId: 'slack-token'
        }
        failure {
            def mensaje = "[César González][${env.JOB_NAME}][${params.selector}] Ejecución fallida en stage [${env.TASK}]"
            slackSend color: 'danger', message: mensaje, tokenCredentialId: 'slack-token'
        }
    }
}
