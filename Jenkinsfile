pipeline{
    agent any
    stages{
        stage("build stage"){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '1c2df7c6-2a93-4470-a322-b94cd1ede707', url: 'https://github.com/ultimateclasses/devopsbatch1.git']])
                sh "mvn clean install"
            }
        }
        stage("docker stage"){
            steps{
                script {
		    sh ""
                    sh "sudo docker build -t suresh-image-local ."
                    sh "sudo docker tag suresh-image-local ultimateclasses2022/devopsbatch1:localversion3"
                }
            }
        }
        stage("dockerhub image push"){
            steps{
                script {
                   // withCredentials([usernamePassword(credentialsId: '1c2df7c6-2a93-4470-a322-b94cd1ede707', passwordVariable: 'dockerhubpass', usernameVariable: 'ultimateclasses2022')]) {
		    //withCredentials([usernameColonPassword(credentialsId: '082de2f8-1135-481d-bffd-bdbe6f01e086', variable: 'dockerhubpass')]) {
                    withCredentials([string(credentialsId: 'dockerid', variable: 'dockerhubpwd')]) {

                    sh 'sudo docker login -u ultimateclasses2022 -p ${dockerhubpwd}'
                    sh "sudo docker push ultimateclasses2022/devopsbatch1:localversion3"
                }
            }
        }
    }
    }
}

