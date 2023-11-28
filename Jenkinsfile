pipeline{
   agent any
   tools{
     maven 'maven'
   }  
   
   environment {
        SCANNER_HOME= tool 'sonar-scanner'
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
    
    stage("maven compile"){
       steps{
         sh 'mvn clean compile'
       } 
    }

    stage("OWASP"){
      steps{
        dependencyCheck additionalArguments: '', odcInstallation: 'DP'
        dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
      }  
    }

   stage('Sonarqube-Analysis') {
            steps {
                sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.url=http://54.89.105.95:9000/ -Dsonar.login=squ_1ec0a9e69d9cb9f1feb0dadec9710e24f97a5c3a -Dsonar.projectName=sonar \
                -Dsonar.java.binaries=. \
                -Dsonar.projectKey=sonar '''
              
            }
        }
  }
}