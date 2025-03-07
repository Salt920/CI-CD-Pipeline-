pipeline {
 agent any
 stages {
 stage('Clone Repository') {
 steps {
 git branch: 'main', url: 'https://github.com/Salt920/CI-CD-Pipeline-.git '
 }
 }

 stage('Deploy Configurations') {
   steps {
      script {
          def exitCode = sh(script: 'wsl ansible-playbook -i ansible/inventory.ini ansible/playbook.yml', returnStatus: true)
          if (exitCode != 0) {
          error("Deployment failed! Blocking push.")
        }
     }
  }
 }
} 
post {
   success {
echo "Deployment successful! Push is allowed."
}
failure {
    echo "Deployment failed! Push is blocked."
    sh 'exit 1'
       }
    }
}


