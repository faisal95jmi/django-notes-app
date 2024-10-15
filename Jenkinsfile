pipeline{
    
 agent any

 stages{
    stage("Code"){
        steps{
            echo "cloning the code"
        git url: "https://github.com/faisal95jmi/django-notes-app.git", branch: "main"
             }
                 }
     
    stage("Build"){
         steps{
        echo "Building the image"
        sh "docker build -t my-note-app ."
             }    }

    stage("push to docker hub"){
         steps{
        echo "pushing the image to docker hub"
        withCredentials([usernamePassword(credentialsId:"jenkinsuser",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
        sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
        sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
        sh "docker push  ${env.dockerHubUser}/my-note-app:latest"
        
        }                 
        }
        }
    stage("Deploy"){
         steps{
        echo "deploying"
        sh "docker-compose down && docker-compose up -d"
             }
    
                   }
}
}
