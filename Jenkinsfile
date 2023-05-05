pipeline {
    agent any
        stages {
        stage('Initialize') {
            steps {
                echo 'Esta es el inicio'
                 script {
                    try {
                        // hacer algo que pueda fallar
                        sh 'echo "La Primera Etapa ha sido completada exitosamente"'
                    } catch (Exception e) {
                        // si algo falla, se registra el error
                        currentBuild.result = 'FAILURE'
                        error "La Primera Etapa ha fallado: ${e.getMessage()}"
                    }
                }
            }
        }
        stage('Build') {
            steps {
                
                script {
                    try {
                        // hacer algo que pueda fallar
                        sh 'echo "La Segunda Etapa ha sido completada exitosamente"'
                        sh 'mvn -B package'
                    } catch (Exception e) {
                        // si algo falla, se registra el error
                        currentBuild.result = 'FAILURE'
                        error "La Segunda Etapa ha fallado: ${e.getMessage()}"
                    }
                }
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

                for (stage in pipeline.stages) {
                    def stageResultColor
                    def stageResultMessage

                    if (stage.state.result == 'SUCCESS') {
                        stageResultColor = '#36a64f'
                        stageResultMessage = "La etapa ${stage.name} ha sido completada exitosamente"
                    } else {
                        stageResultColor = '#FF0000'
                        stageResultMessage = "La etapa ${stage.name} ha fallado"
                    }

                    slackSend(color: stageResultColor, message: stageResultMessage)
                }
        //     slackSend( channel: '#fundamentos-de-devops', color: '#00FFFF',  message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} by ${env.BUILD_USER}\n More info at: ${env.BUILD_URL} ${env.STAGE_NAME}")
        // }
        }
    }
}
}
