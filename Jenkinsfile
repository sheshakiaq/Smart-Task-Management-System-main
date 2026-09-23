pipeline{
  agent any
  
  tools{
    nodejs 'Nodejs-Id'
  }
  
  stages{
    stage('checkout'){
      steps{
        git branch: 'main',
          url: 'https://github.com/sheshakiaq/Smart-Task-Management-System-main.git'
      }
    }      
    stage('Cloning'){
      steps{
        echo "Repo Cloned ..."
      }
    }
    
    stage('Install Dependencies'){
      steps{
        echo "Installing npm denpendecies"
        sh '''
          node --version
          npm --version
          cd frontend 
          npm install
        '''
        echo "npm installed"
      }
    }
    
    stage('Test NPM'){
      steps{
        echo ('Testing NPM..')
        sh '''
          cd frontend
          npm run
        '''
        echo 'Test Completed'
      }
    }
   
    stage('Sonarqube Analysis') {
            steps {
              echo 'Sonarqube process '
                script {
                    def scannerhome = tool name: 'sonar-scanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                    
                withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                    sh """
                            ${scannerhome}/bin/sonar-scanner \
                            -Dsonar.projectKey=devops-flow \
                            -Dsonar.sources=frontend\
                            -Dsonar.host.url=http://localhost:9000 \
                            -Dsonar.login=${SONAR_TOKEN}
                       """
                    }
                   
                 echo 'Sonarqube Process Success'
                } 
            }
        }
    stage('Quality Gate') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: false
                }
            }
        }
        
  }
}
