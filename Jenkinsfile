pipeline {
    agent any
        stages {
            stage('Initialize') {
                steps {
                    script {
                        echo 'Esta es el inicio'
                        if (currentBuild.result == 'SUCCESS') {
                        slackSend message: 'Compleado'
                        } else {
                        slackSend message: 'Fallido'
                        }
                    }
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
                slackSend(channel: '@U05690FEL7P', message: 'Comenzando desde 0')
            }
        }
    }
}
