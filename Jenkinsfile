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
                            if(expn != 'null'){
                                echo "it was upstream"
                               
                            }
                            else {
                                echo "it was a manual trigger"
                                def data = readFile(file: 'Flag')
                                println(data.charAt(0))
                                if(data.charAt(0) == '1')
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
