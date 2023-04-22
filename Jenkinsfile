@Library('my-shared-library')_
pipeline{

   agent any
   parameters {
      choice (name: 'action', choices: 'create\ndelete', description: 'create/Destroy')
      string (name: 'ImageName', description: 'name of the dockerfile', defaultValue: 'javapp')
      string (name: 'ImageTag', description: 'tag of the dockerfile', defaultValue: 'v1')
      string (name: 'dockerHubUser', description: 'name of the dockeruser', defaultValue: 'rajeshjallu')
   }
   stages {
        stage ('Git Checkout') {
               when { expression { params.action == 'create'} }
           steps {
           gitCheckout(
              branch: "dev",
              url: "https://github.com/rajesh1218/mrdevops_java_app.git"
            )
            }
        }
        stage ('unit test maven'){
        when { expression { params.action == 'create'} }    
            steps {
                script{
                    mvnTest()
                }
            }
        }
        stage ('Intergartion test maven'){
        when { expression { params.action == 'create'} }    
            steps {
                script{
                    mvnIntegrationTest()
                }
            }
        }
        stage ('Build maven: maven'){
        when { expression { params.action == 'create'} }    
            steps {
                script{
                    mvnBuild()
                }
            }
        }
        stage ('Docker image: Build'){
        when { expression { params.action == 'create'} }    
            steps {
                script{
                    dockerBuild("${params.ImageName}","${params.ImageTag}","${params.dockerHubUser}")
                }
            }
        }
        stage ('Docker image Scan: Trivy'){
        when { expression { params.action == 'create'} }    
            steps {
                script{
                    dockerImageScan("${params.ImageName}","${params.ImageTag}","${params.dockerHubUser}")
                }
            }
        }
        stage ('Docker image psuh: Dockerhub'){
        when { expression { params.action == 'create'} }    
            steps {
                script{
                    dockerImagePush("${params.ImageName}","${params.ImageTag}","${params.dockerHubUser}")
                }
            }
        }

    }
}
