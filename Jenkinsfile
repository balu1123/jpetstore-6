pipeline {
    agent any
    tools{
        
        maven  'maven'
    }
    
    environment{
        SCANNER_HOME= tool 'sonar-scanner'
    }

    stages {
        stage("Git Checkout"){
            steps {
                git branch: 'master', changelog: false, poll: false, url: 'https://github.com/balu1123/jpetstore-6.git'
            }
        }

        stage("COMPILE"){
            steps {
                sh "mvn clean compile"
            }
        }

        stage("Build"){
            steps {
                sh "mvn clean package -DskipTests=true"
            }
        }

        stage("OWASP"){
          steps{
            dependencyCheck additionalArguments: '', odcInstallation: 'DP'
            dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
          }  
        }
        
        stage("Sonarqube") {
            steps {
                withSonarQubeEnv('sonar-scanner'){
                   sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=petstore \
                   -Dsonar.java.binaries=. \
                   -Dsonar.projectKey=petstore '''
               }
            }
        }

         /*stage("Nexus"){
          steps{
            withMaven(globalMavenSettingsConfig: 'global-settings-xml') {
     
            sh 'mvn deploy -DskipTests=true'   
              }
            
          }  
        }*/
    }
}       
