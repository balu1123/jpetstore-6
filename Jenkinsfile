pipeline{
   agent any
   tools{
     jdk 'jdk17'
     maven 'maven'
   }  
        
  stages{
    stage ('clean Workspace'){
            steps{
                cleanWs()
            }
         }  

    stage("Git checkout"){
      steps{
        script{
          git changelog: false, poll: false, url: 'https://github.com/balu1123/jpetstore-6.git'
        }
      }  
    }

    stage("maven compile"){
       steps{
         sh 'mvn clean compile'
       } 
    }

    stage("UNIT Test"){
      steps{
        sh 'mvn test'
      }  
    }
  
  }
}
    