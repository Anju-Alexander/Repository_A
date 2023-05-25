pipeline {
    agent any

    stages {
        stage('Clone A') {
            steps {
                echo 'Clone A'
                git branch: 'main', credentialsId: 'cf3d6d86-2ff7-465a-8767-58e572a16539', url: 'https://github.com/Anju-Alexander/Repository_A.git'
                   
            }
            
        }
        stage('Update to Latest Version')
        {
            steps{
                sh 'mvn versions:use-next-versions -Dincludes=org.beginsecure.domain.primitives:CustomJar'
                echo 'updated pom.xml to new version'
            }
        }
       
        stage('Build') {
            steps {
               
                    echo 'Build'
                    sh 'mvn clean install'
                    echo 'Build stable'
                
            }
        }
    }
}
