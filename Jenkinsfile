pipeline{
   environment {

       def imageName = "7263958869/test-repo:apche-${env.BRANCH_NAME}-v0.0-${env.BUILD_ID}"


   }


   agent any
   stages{

     
       stage("Build Docker Image") {
         steps{
           script {
             
                 sh "sudo docker build --network=host -t ${imageName} ."
               
           }
         }
       }

       stage("Push Image to Registry") {
         steps{
           script {
             
                 sh "sudo docker push ${imageName}"
                 sh "sudo docker rmi --force \$(docker images -q ${imageName} | uniq)"
                
           }
         }
       }

     

   }
   

 
}
