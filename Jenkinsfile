pipeline {
    agent any

    stages {
        stage('Clone A') {
            steps {
                echo 'Clone A'
                git branch: 'main', credentialsId: 'cf3d6d86-2ff7-465a-8767-58e572a16539', url: 'https://github.com/Anju-Alexander/Repository_A.git'
                   
            }
            
        }
        stage('Update, Build & Push')
        {
            steps{
                
                    script {
                        def expn="${currentBuild.getBuildCauses()[0].upstreamProject}"
                        
                    }   
               
                
                echo "Build Caused by ${expn}"
               
               
            }
        }
       
        
    }
}
