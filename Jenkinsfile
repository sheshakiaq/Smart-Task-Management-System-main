pipeline{
  agent any
  
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
          cd frontend && npm install
        '''
        echo "npm installed"
      }
    }
  }
}
