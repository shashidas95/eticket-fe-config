pipeline {
    agent any

    parameters {
        string(name: 'IMAGE_TAG', description: 'Enter the image tag')
    }
    
    environment {

        GIT_REPO = "https://github.com/shashidas95/eticket-fe-config" 
        APP_NAME = "eticket-fe"

    }

    stages{

        stage('CLEANUP WORKSPACE'){
            steps{
                script{
                    cleanWs()
                }
            }
        }

        stage("CHECKOUT GIT REPO"){
            steps{
                git branch: 'master', url: "${GIT_REPO}"
            }
        }

        stage("UPDATE K8S DEPLOYMENT FILES AND PUSH TO THE GIT REPO"){
            steps{

                sh 'cat ./k8s/deployment.yaml'
                sh "sed -i '' 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' ./k8s/deployment.yaml"
                sh 'cat ./k8s/deployment.yaml'

                sh 'git config --global user.email shashidas95@gmail.com'
                sh 'git config --global user.name shashidas95'
                sh 'git add ./k8s/deployment.yaml'
                sh "git commit -m 'Updated deployment files to ${IMAGE_TAG}'"

                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'pass', usernameVariable: 'uname')]) {
                    sh 'git push https://$uname:$pass@github.com/shashidas95/eticket-fe-config.git master'
                }
            }
        }
    }
}