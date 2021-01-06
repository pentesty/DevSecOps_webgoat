pipeline {
  agent any 
  tools {
    maven 'Maven'
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
    
    stage ('OWASP Dependency-Check Vulnerabilities') {
            steps {
                dependencyCheck additionalArguments: ''' 
                    -o "./" 
                    -s "./"
                    -f "ALL" 
                    --prettyPrint''', odcInstallation: 'OWASP-DC'

                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
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
