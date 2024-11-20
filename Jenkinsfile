pipeline{
    agent any
    stages{
        stage("build stage"){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '1c2df7c6-2a93-4470-a322-b94cd1ede707', url: 'https://github.com/ultimateclasses/devopsbatch1.git']])
                sh "mvn clean install"
            }
        }
    }
}
