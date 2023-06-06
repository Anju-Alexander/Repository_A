pipeline {
    agent any

    stages {
            stage('Clone A') {
                steps {
                    echo 'Clone A'
                    git branch: 'main', credentialsId: 'cf3d6d86-2ff7-465a-8767-58e572a16539', url: 'https://github.com/Anju-Alexander/Repository_A.git'
                  

                }

            }
        
         
            stage('Check')
            {
               steps {
                    currentBuild.result = 'ABORTED'
                    error('Aborting the build')
                    return
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

                                sh 'git remote add repo_a_push https://github.com/Anju-Alexander/Repository_A.git'
                                sh 'git checkout -b latest-\"${BUILD_NUMBER}\"'
                                writeFile(file: 'Flag', text: "0")
                                sh 'git add pom.xml'
                                sh 'git add Flag'
                                sh 'git commit -m "updated Repo A version"'
                                sh 'git push -u repo_a_push latest-\"${BUILD_NUMBER}\"'
                                sh 'git remote rm repo_a_push'
                                slackSend channel: 'repo-a-notifications', message: "Latest build of Repo A has been successful and it is present in branch latest-${BUILD_NUMBER}!!", tokenCredentialId: 'b4c53875-29c5-4f3a-a5dc-5a97790ff44e'

                               
                            }
                            else {
                                echo "it was a manual trigger"
                                def dir1 = sh(script:'mvn versions:display-dependency-updates | grep "CustomJar"', returnStatus:true, returnStdout:true)
                                println(dir1)
                                
                                
                                if(dir1 == 0)
                                {
                                    echo "Updates to CustomJar dependencies are available!!"
                                }
                             
                            }   
                            commit = sh(returnStdout: true, script: 'git log -1 --oneline').trim()
                            
                            commitMsg = commit.substring( commit.indexOf(' ') ).trim()
                            
                            println(commitMsg.contains('Anju'))

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
