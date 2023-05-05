pipeline{
    agent any
    tools{
        maven "maven3.8.8"
    }
    
    stages{
      stage("1. clone repo"){
          steps{
              sh "echo start cloning "
              git branch: 'main', credentialsId: 'tomcat-cred', url: 'https://github.com/floatt1/web-app.git'
              sh "echo end clone"
          
      }
     }
     
     stage("2. build with maven"){
         steps{
            sh "echo start build"
            sh "mvn clean package"
         }
     }
     stage("3. code scan"){
        steps{
            sh "mvn sonar:sonar"
            
            
        } 
    }
       /*
        stage("4. store in artifactory"){
            steps{
                sh "mvn deploy"
  
        }
           }
         */  
           stage("5. deploy to tomcat"){
               steps{
                   sh "echo deploy to tomcat"
                   deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://52.91.234.153:9000')], contextPath: null, war: 'target/*.war'
               }
           }
            
   }
}  
