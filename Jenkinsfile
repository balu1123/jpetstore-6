pipeline{
   agent any
   tools{
     jdk 'jdk1.8'
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
   }
}