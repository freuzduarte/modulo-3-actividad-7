pipeline {
    agent any
        stages {
        stage('Initialize') {
            steps {
                echo 'Esta es el inicio'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn clean verify'
            }
        }

        }

    post {
        always {
            script {
                echo 'I will always say Hello again!'


                def resultColor
                def resultMessage

                // determinar el resultado del pipeline
                if (currentBuild.result == 'SUCCESS') {
                    resultColor = '#36a64f'
                    resultMessage = 'El pipeline se ha ejecutado correctamente'
                } else {
                    resultColor = '#FF0000'
                    resultMessage = 'El pipeline ha fallado'
                }

                
                // enviar mensaje a Slack con el resultado del pipeline
                slackSend(color: resultColor, message: resultMessage)

                // enviar mensaje a Slack con el resultado de cada etapa
                slackSend(color: resultColor, message: 'Resultados de las etapas:')

                slackSend(channel: '@U05690FEL7P', message: 'Comenzando desde 0')
        //     slackSend( channel: '#fundamentos-de-devops', color: '#00FFFF',  message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} by ${env.BUILD_USER}\n More info at: ${env.BUILD_URL} ${env.STAGE_NAME}")
        // }
        }
    }
}
}
