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
    stage('Build Frontend'){
      steps{
        echo 'Bulding React project'
        sh '''
          cd frontend
          npm run build
        '''
      }
    }
   stage('Deploy S3 Bucket'){
     steps{
       withCredentials([
         usernamePassword(
           credentialsId: 'floci-id',
           usernamwVariable: 'AWS_ACCESS_KEY_ID',
           passwordVariable: 'AWS_SECRET_ACCESS_KEY'
         )
       ]){
         echo 'updating S3 Bucket'
       sh ''' 
         aws --endpoint-url=http://172.17.0.2:4566 \
         s3 sync frontend/dist/ \
         s3://devops-flow-task/ \
         --delete 
       '''
       echo 'Frontend Uploaded Successfully'
       }      
     }
   }
  }
}
