@Library('my-shared-library')_
pipeline{

agent any
   stages {
        stage ('Git Checkout') {
           steps {
           gitCheckout(
              branch: "dev",
              url: "https://github.com/rajesh1218/mrdevops_java_app.git"
            )
            }
        }
        stage ('unit test maven'){
            steps {
                script{
                    mvnTest()
                }
            }
        }
        stage ('Intergartion test maven'){
            steps {
                script{
                    mvnIntegrationTest()
                }
            }
        }
    }
}
    

   