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
    stage ('Check-content') {
      steps {
        sh 'ls -la'
      }
    }
    
    stage ('Build') {
      steps {
      sh 'mvn clean install'
       }
    }
  
    
    stage ('check') {
      steps {
         sh 'ls -la'
      }
    }
   }  
}
