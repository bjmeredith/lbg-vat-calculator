pipeline {
  agent any

  stages {
    stage('Checkout') {
        steps {
          // Get some code from a GitHub repository
          git branch: 'main', url: 'https://github.com/bjmeredith/lbg-vat-calculator.git'
        }
    }
    stage('SonarQube Analysis') {
      environment {
        scannerHome = tool 'sonarqube'
      }
        steps {
            withSonarQubeEnv('sonar-qube-1') {        
              sh "${scannerHome}/bin/sonar-scanner"
            }   

        }

    }


    stage('SonarQube Quality Gate') {
      environment {
        scannerHome = tool 'sonarqube'
      }
        steps {

            timeout(time: 10, unit: 'MINUTES'){
            waitForQualityGate abortPipeline: true
           }

        }

    }




  }
}