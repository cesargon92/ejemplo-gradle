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
            slackSend color: 'good', message: "[César González][${env.JOB_NAME}][${params.selector}] Ejecución exitosa", tokenCredentialId: 'slack-token'
        }
        failure {
            slackSend color: 'danger', message: "[César González][${env.JOB_NAME}][${params.selector}] Ejecución fallida en stage [${env.TASK}]", tokenCredentialId: 'slack-token'
        }
    }
}
