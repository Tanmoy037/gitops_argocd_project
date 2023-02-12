pipeline{

    agent any

    environment{

        DOCKERHUB_USERNAME = "tanmoy037"
        APP_NAME = "gitops-args-app"
        IMAGE_TAG = "${BUILD_NUMBER}"
        IMAGE_NAME = "${DOCKERHUB_USERNAME}" + "/" + "${APP_NAME}"
        REGISTRY_NAME = 'dockerhub'
    }

    stages{

        stage('Clenup workspace'){

            steps{
                script{

                    cleanWs(deleteDirs: true, excludeDirs: [])
                    }
                }
            }
            stage('Checkout SCM'){

                steps{
                    script{
                        git credentialsId: 'github',
                        url: 'https://github.com/Tanmoy037/gitops_argocd_project.git'
                        branch: '/main'  
                    }   
                }
            }
        }

}

