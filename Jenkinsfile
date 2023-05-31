def env = build.environment
def cause = env.BUILD_CAUSE_UPSTREAMTRIGGER
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
                
               
                echo cause
                echo "Build Caused by ${currentBuild.getBuildCauses()[0].userId}"
               
               
            }
        }
       
        
    }
}
