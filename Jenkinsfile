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
                slackSend(channel: '@U05690FEL7P', message: "Comenzando *${currentBuild.currentResult}:* build ${env.BUILD_NUMBER}, ${env.JOB_NAME}")
            }
        }
    }
}
