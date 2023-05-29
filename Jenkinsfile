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
                
                def upstream_project = "${currentBuild.getBuildCauses()[0].upstreamProject}"
                echo "Build Caused by ${upstream_project}"
                sh 'mvn versions:use-latest-versions -Dincludes=org.beginsecure.domain.primitives:CustomJar'
                echo 'updated pom.xml to new version'
                echo 'Build'
                sh 'mvn clean install'
                echo 'Build stable'
                sh 'git checkout -b latest-\"${BUILD_NUMBER}\"'
                sh 'git remote add repo_a_push https://github.com/Anju-Alexander/Repository_A.git'
                sh 'git add pom.xml'
                sh 'git commit -m "updated Repo A version"'
                sh 'git push -u repo_a_push latest-\"${BUILD_NUMBER}\"'
                
                sh 'git remote rm repo_a_push'
               
            }
        }
       
        
    }
}
