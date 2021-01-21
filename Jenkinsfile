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
      sh 'cd /dumpster_diver/DumpsterDiver/ ; sudo python3 DumpsterDiver.py -p ${WORKSPACE} -o DumpsterDiver_output'
      sh 'trufflehog3 https://github.com/Suyashk96/webGoat_java.git -f html -o truffelhog_output || true'
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
         sh 'sudo docker run -t owasp/zap2docker-stable zap-baseline.py -t http://192.168.0.106/WebGoat/ > zap_output'
         sh 'cat zap_output'
         sh 'cd /arachni/arachni-1.5.1-0.5.12/bin/; sudo ./arachni http://192.168.0.106/WebGoat --report-save-path=DAST.afr'
      }
    }
   }  
}
