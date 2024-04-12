pipeline {
    agent {
        label "jenkins-agent"
    }
    environment {
        APP_NAME = "complete-prodcution-e2e-pipeline"
    }

    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }

        stage("Checkout from SCM") {
            steps {
                git branch: 'main', credentialsId: 'github-pat', url: 'https://github.com/daoducan/gitops-test-ci-cd-pipeline'
            }
        }

        stage("Update the Deployment Tags") {
            steps {
                sh """
                    cat deployment.yaml
                    sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yaml
                    cat deployment.yaml
                """
            }
        }
/*
        stage("Push the changed deployment file to Git") {
            steps {
                sh """
                    git config --global user.name "daoducan88"
                    git config --global user.email "daoducan88@gmail.com"
                    git add deployment.yaml
                    git commit -m "Updated Deployment Manifest"
                """
                withCredentials([gitUsernamePassword(credentialsId: 'github-pat', gitToolName: 'Default')]) {
                    sh "git push https://github.com/daoducan/gitops-test-ci-cd-pipeline main"
                }
            }
        }*/

        stage("Push the changed deployment file to Git") {
            steps {
                withCredentials([gitUsernamePassword(credentialsId: 'github-pat', gitToolName: 'Default')]) {
                    sh """
                        git config --global user.name "daoducan"
                        git config --global user.email "daoducan1991@gmail.com"
                        git add deployment.yaml
                        git commit -m "Updated Deployment Manifest"
                        git push https://github.com/daoducan/gitops-test-ci-cd-pipeline main
                    """
                }
            }
        }
    }
}