pipeline {
    agent any
        environment{
            HOLA = 'ESTO ES UNA VARIABLE'
        }
        stages {
            stage('Initialize') {
                steps {
                    script {
                        echo 'Esta es el inicio'
                    }
                }
            }
            stage('Build') {
                steps {
                    script {
                        sh 'mvn -B package'
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
                slackSend(channel: '@U05690FEL7P', message: "Comenzando desde 0, *${currentBuild.currentResult}:* build ${env.BUILD_NUMBER}, ${env.JOB_NAME}, ")
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
            }
        }
    }
}
