pipeline{
   environment {

       def imageName = "7263958869/test-repo:apche-${env.BRANCH_NAME}-v0.0-${env.BUILD_ID}"


   }


   agent any
   stages{

     
       stage("Build Docker Image") {
         steps{
           script {
             
                 sh "docker build --network=host -t ${imageName} ."
               
           }
         }
       }

       stage("Push Image to Registry") {
         steps{
           script {
             
                 sh "docker push ${imageName}"
                 sh "docker rmi --force \$(docker images -q ${imageName} | uniq)"
                
           }
         }
       }

     

   }
   
   
       post {

       success{
           mail to: 'sumit.dharne@afourtech.com',
            subject: "[JENKINS]: ${currentBuild.fullDisplayName} Succeed",
            body: "Project Name : ${currentBuild.fullDisplayName}\n  Status       : Succeed\n  Log          : ${env.BUILD_URL}/consoleText"
           }

       failure{
          mail to: 'sumit.dharne@afourtech.com',
            subject: "[JENKINS]: ${currentBuild.fullDisplayName} Failed",
            body: "Project Name : ${currentBuild.fullDisplayName}\n  Status       : Failed\n  Log          : ${env.BUILD_URL}/consoleText"
       }
   }

 
}
