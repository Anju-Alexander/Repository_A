pipeline {
    agent any

    stages {
            stage('Clone A') {
                steps {
                    echo 'Clone A'
                    git branch: 'main', credentialsId: 'cf3d6d86-2ff7-465a-8767-58e572a16539', url: 'https://github.com/Anju-Alexander/Repository_A.git'
                    echo "the  path is"
                    sh 'pwd'
                   

                }

            }
            stage('Update, Build & Push')
            {
                steps{

                        script {
                            def expn="${currentBuild.getBuildCauses()[0].upstreamProject}"
                            if(expn != 'null'){
                                echo "it was upstream"
                                sh 'mvn versions:use-latest-versions -Dincludes=org.beginsecure.domain.primitives:CustomJar'
                                echo 'updated pom.xml to new version'
                                echo 'Build'
                                sh 'mvn clean install'
                                echo 'Build stable'
                                writeFile(file: 'Flag', text: "0")
                                sh 'git checkout -b latest-\"${BUILD_NUMBER}\"'
                                sh 'git remote add repo_a_push https://github.com/Anju-Alexander/Repository_A.git'
                                sh 'git add pom.xml'
                                sh 'git add Flag'
                                sh 'git commit -m "updated Repo A version"'
                                sh 'git push -u repo_a_push latest-\"${BUILD_NUMBER}\"'
                                sh 'git remote rm repo_a_push'
                                slackSend channel: 'repo-a-notifications', message: "Latest build of Repo A has been successful and it is present in branch latest-${BUILD_NUMBER}!!", tokenCredentialId: 'b4c53875-29c5-4f3a-a5dc-5a97790ff44e'

                            }
                            else {
                                echo "it was a manual trigger"
                                def data = readFile(file: 'Flag')
                                println(data.charAt(0))
                                if(data == '1')
                                {
                                    echo "Updates to CustomJar dependencies are available!!"
                                }
                             
                            }   

                        }   


                    }
                }

        }
    post {
        always {
          echo "I will always execute this!"      
                                      

        
        }   
      }
}
