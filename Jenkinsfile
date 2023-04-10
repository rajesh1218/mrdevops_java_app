@Library('my-shared-library') _

pipeline{

    agent any
stage ('Git Checkout'){
    steps {
        script {
            git branch: 'dev', url: 'https://github.com/rajesh1218/mrdevops_java_app.git'
        }
    }
 }
 
}
    

   