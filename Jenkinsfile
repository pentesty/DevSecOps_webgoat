pipeline {
  agent any 
  tools {
    maven 'Maven'
    dependency-check "OWASP-DC"
  }
  stages {
    stage ('Initialize') {
      steps {
        sh '''
                echo "PATH = ${PATH}"
                echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
    
    stage ('Build') {
      steps {
        sh 'mvn clean install -DskipTests'
      }
    }
    
    
    stage('Dependency Check') {
        steps {
            // Run OWASP Dependency Check
            dependencyCheck additionalArguments: '-f "HTML, XML,CSV" -s .'
        }
      }
   
    
    stage ('Run') {
      steps {
      sh 'nohup java -jar webgoat-server/target/webgoat-server-v8.2.0-SNAPSHOT.jar &'
       }
    }
  
    
    stage ('DAST') {
      steps {
         sh 'ls -la'
      }
    }
   }  
}
