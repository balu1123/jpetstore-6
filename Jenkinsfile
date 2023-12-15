pipeline{
   agent any
   tools{
     
     maven 'maven'
   }  

   environment {
        scannerHome = tool 'sonar'
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

    stage("Sonarqube Analysis "){
            steps{
                withSonarQubeEnv('sonar-scanner') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner 
                    -Dsonar.projectName=Petshop \
                    -Dsonar.java.binaries= **/*.java
                    -Dsonar.projectKey=Petshop '''
                }
            }
        }
  
  }
}
    