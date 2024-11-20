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
    stages{
        stage("docker stage"){
            steps{
                script {
                    sh "docker build -t suresh-image-local ."
                    sh "docker tag suresh-image-local ultimateclasses2022/devopsbatch1:localversion3"
                }
            }
        }
    }
    stages{
        stage("dockerhub image push"){
            steps{
                script {
                    withCredentials([usernamePassword(credentialsId: '1c2df7c6-2a93-4470-a322-b94cd1ede707', passwordVariable: 'dockerhubpass', usernameVariable: 'ultimateclasses2022')]) {
                    sh "docker login -u $usernameVariable -p $dockerhubpass"
                    sh "docker push ultimateclasses2022/devopsbatch1:localversion3"
                }
            }
        }
    }
}
}

