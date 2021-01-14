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
    
    stage ('Check secrets in repository') {
      steps {
      sh 'trufflehog3 `pwd` --rules regex.json -f html -o truffelhog_output'
      sh 'python3 /dumpster_diver/DumpsterDiver/DumpsterDiver.py -p `pwd` -o DumpsterDiver_output'
      sh 'ls'
      }
    }
    
    stage ('Install dependencies') {
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
    
    stage ('Static analysis with sonarqube') {
      steps {
        withSonarQubeEnv('sonar') {
          sh 'mvn sonar:sonar'
        }
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
