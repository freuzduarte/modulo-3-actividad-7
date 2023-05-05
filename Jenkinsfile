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
                        success{
                            slackSend message: "Comenzando el Proyecto"
                        }
                        failure{
                            slackSend message: "Proyecto Fallido"
                        }
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
                slackSend(channel: '@U05690FEL7P', message: "Comenzando desde 0, *${currentBuild.currentResult}:* build ${env.BUILD_NUMBER}, ${env.JOB_NAME}")
            }
        }
    }
}
