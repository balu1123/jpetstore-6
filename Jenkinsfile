pipeline{
   agent any
   tools{
     maven 'maven'
   }  

   stages{
    stage("Git checkout"){
      steps{
        script{
          git changelog: false, poll: false, url: 'https://github.com/balu1123/jpetstore-6.git'
        }
      }  
    }

    stage("UNIT Test"){
      steps{
        sh 'mvn test'
      }  
    }
    
    stage("maven"){
       steps{
         sh 'mvn -Dcargo.servlet.port=8080 cargo:start'
       } 
    }
  }
}