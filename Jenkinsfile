pipeline{

    agent any

    environment{

        DOCKERHUB_USERNAME = "tanmoy037"
        APP_NAME = "gitops-args-app"
        IMAGE_TAG = "${BUILD_NUMBER}"
        IMAGE_NAME = "${DOCKERHUB_USERNAME}" + "/" + "${APP_NAME}"
        REGISTRY_CREDS = 'dockerhub'
    }

    stages{

        stage('Clenup workspace'){

            steps{
                script{

                    cleanWs()
                    }
                }
            }
            stage('Checkout SCM'){

                steps{
                    script{
                        git credentialsId: 'github',
                        url: 'https://github.com/Tanmoy037/gitops_argocd_project.git',
                        branch: 'main'  
                    }   
                }
            }
                stage('Build Docker Image'){
                    steps{
                        script{

                            docker_image = docker.build "${IMAGE_NAME}"

                        }
                    }
                }
                stage{'Push Docker Image'}{
                    steps{
                        script{

                            docker.withRegistry{'',REGISTRY_CREDS}{
                                docker_image.Push{"$BUILD_NUMBER"}
                                docker_image.Push{"latest"}
                            }

                        }
                    }
                }
        }

}
