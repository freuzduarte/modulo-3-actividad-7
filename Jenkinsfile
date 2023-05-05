pipeline {
    agent any
        stages {
            stage('Initialize') {
                steps {
                    script {
                        echo 'Esta es el inicio'
                        slackSend(message: "Comenzando el Proyecto 👌 ${env.JOB_NAME} ", color: 'good')
                    }
                }
            }
            stage('Build') {
                steps {
                    script {
                        sh 'mvn -B package'
                        if (currentBuild.result == 'FAILURE') {
                        slackSend(message: "Error al compilar 🤡 ${env.JOB_NAME} ", color: '#CD5C5C')
                        }else {
                        slackSend(message: "Compilado Perfectamente 🥵 ${env.JOB_NAME} ", color: '#3633FF')
                        }
                    }
                }
            }

            stage('Test') {
                steps {
                    script {
                        sh 'mvn clean verify'
                        if (currentBuild.result == 'FAILURE') {
                        slackSend(message: "Error al hacer test 🤡 ${env.JOB_NAME} ", color: '#CD5C5C')
                            }else {
                        slackSend(message: "Test Completado sin errores 🥵 ${env.JOB_NAME} ", color: '#3633FF')
                        }
                    }
                }
            }
        }

    post {
        always {
            script {
                echo 'Prueba'

                if (currentBuild.result == 'SUCCESS') {
                    slackSend(channel: '@U05690FEL7P', message: "Finalizado*${currentBuild.currentResult}:* build ${env.BUILD_NUMBER}, ${env.JOB_NAME}", color: '#CD5C5C')
                }else if (currentBuild.result == 'FAILURE') {
                    slackSend(channel: '@U05690FEL7P', message: "Error al Crear el proyecto *${currentBuild.currentResult}:* build ${env.BUILD_NUMBER}, ${env.JOB_NAME}", color: '#FF0017')
                }
            }
        }
    }
}
