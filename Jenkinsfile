pipeline{
    agent any

    stages{
      stage('checkout'){
        steps{
          echo 'Fetching Source Code'
          checkout scm
          }
        }
    stage ('Code quality check!'){
        steps{
          echo 'Checking Code quality'
          bat '''
          findstr GOOD quality.txt > nul
          if errorlevel 1 (
              echo Code Quality Failed
              exit
          ) else (
              echo Code Quality Passed
            ) '''
        }
    }
  stage ('Generate Report'){
    steps {
      echo 'Generating build report'
      bat '''
      mkdir reports
      echo Build Sucessfull > reports\\build-report.txt
      '''
      }
    }

      stage ('Archive Artifacts') {
        steps{
          echo 'Archiving reports'
          archiveArtifacts artifacts: 'reports/*.txt' , fingerprint: true 
        }
      }
  post {
      sucess {
        echo 'Pipeline completed successfully'
}
    failure {
      echo 'Pipeline failed- code blocked'
    }
  }
}
}
