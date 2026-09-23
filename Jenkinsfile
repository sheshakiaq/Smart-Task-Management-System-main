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
          npm test --run
        '''
        echo 'Test Completed'
      }
    }
  }
}
