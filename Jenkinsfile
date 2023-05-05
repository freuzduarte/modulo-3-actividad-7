pipeline {
    agent any
        stages {
        stage('Initialize'){
            steps{
                echo "Esta es el inicio"
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B package'
            
            }
        }
            
        stage('Test') {
            steps {
                 sh "mvn clean verify" 
            
            }
        } 
        // stage("Publish to Nexus Repository Manager") {
        //     steps {
        //         script {
        //             pom = readMavenPom file: "pom.xml";
        //             filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
        //             echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
        //             artifactPath = filesByGlob[0].path;
        //             artifactExists = fileExists artifactPath;
        //             if(artifactExists) {
        //                 echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
        //                 nexusArtifactUploader(
        //                     nexusVersion: "nexus3",
        //                     protocol: "http",
        //                     nexusUrl: "192.168.26.129:8081",
        //                     groupId: pom.groupId,
        //                     version: pom.version,
        //                     repository: "maven-releases",
        //                     credentialsId: "admin",
        //                     artifacts: [
        //                         [artifactId: pom.artifactId,
        //                                 classifier: '',
        //                                 file: artifactPath,
        //                                 type: pom.packaging]
        //                     ]
        //                 );
        //             } else {
        //                 error "*** File: ${artifactPath}, could not be found";
        //             }
        //         }
        //     }
        
        //     } 
     }
     post{
        always {
             slackSend( channel: "#fundamentos-de-devops", color: "#00FFFF",  message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} by ${env.BUILD_USER}\n More info at: ${env.BUILD_URL} ${env.NODE_LABELS}" , iconEmoji: "🥵")
        }
        // success{
        //     slackSend( channel: "#fundamentos-de-devops", color: "#008f39", message: "Funcionando Perfectamente (<${env.BUILD_URL}|Open>)", iconEmoji: "🥵🥵")
        // }
        // failure{
        //     slackSend( channel: "#fundamentos-de-devops", color: "#ff0000", message: "Fallando todo (<${env.BUILD_URL}|Open>)", iconEmoji: "🤡💀")
        // } 
    }
}
