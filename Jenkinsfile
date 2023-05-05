pipeline {
    agent any
    environment {
        CHANNEL = '#fundamentos-de-devops'
        GROUP = 'sustantivagrupo'
    }
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
                slackSend(channel: '@Uzcategui', message: 'Comenzando desde 0')
        //     slackSend( channel: '#fundamentos-de-devops', color: '#00FFFF',  message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} by ${env.BUILD_USER}\n More info at: ${env.BUILD_URL} ${env.STAGE_NAME}")
        // }
        }

    // success{
    //     slackSend( channel: "#fundamentos-de-devops", color: "#008f39", message: "Funcionando Perfectamente (<${env.BUILD_URL}|Open>)", iconEmoji: "🥵🥵")
    // }
    // failure{
    //     slackSend( channel: "#fundamentos-de-devops", color: "#ff0000", message: "Fallando todo (<${env.BUILD_URL}|Open>)", iconEmoji: "🤡💀")
    // }
    }
}
}
