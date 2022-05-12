pipeline{
    agent none
    stages{
        stage('Build'){
            agent{
                docker{ image 'maven:3.8.1-adoptopenjdk-11'}
            }
            steps{
                sh 'mvn --version'
            }
        }
        stage('Test'){
            agent{
                docker{ image 'node:16-alpine'}
            }
            steps{
                sh 'exit 1'
            }
            post {
                always {
                    echo "Post-Test result: ${currentBuild.result}"
                    echo "Post-Test currentResult: ${currentBuild.currentResult}"
                }
                failure{
                    emailext(attachLog: true, body: 'Fallimento in fase di Test' , subject: 'Fallimento Test ramo feature', to: 'fabiosirugo8@gmail.com')
                }
            }
        }
        stage('Deploy'){
            when{
                expression{
                    !("SUCCESS".equals(currentBuild.previousBuild.result))
                }

                //Capire come concatenare i vari stage usando una sintassi adeguata... In questa prova ho utilizzato currentBuild.previousBuild.result
                //per motivi di privilegi
                //Se lo stage precedente fallisce quelli successivi non verranno eseguiti. (chiedere direttamente deploy senza effettuare un controllo?)

                // !("SUCCESS".equals(currentBuild.previousBuild.result))
                //This will allow you to see the result of the previous build without needing 
                //to have any special privileges set by the Jenkins administrator. It should be able to be run anywhere.

                /*
                input {
                    message "La build è avvenuta con successo vuoi procedere al deploy?"
                    ok "Effettua Deploy"
                    parameters {
                        string(defaultValue: 'ok', name: 'Next_Step', trim: true) 
                    }
                }
                */
            }
        
            steps{
                echo "I'm deploying i'm not in master branch"
            }
        }
        stage('Hotfix esempio'){
            when{
                branch'hotfix'
            }
            agent{
                docker{ image 'node:16-alpine'}
            }
            steps{

                sh 'node --version'
                echo "I'm in hotfix"
            }
        }
        
    }
    post {
        always {
            echo "Pipeline result: ${currentBuild.result}"
            echo "Pipeline currentResult: ${currentBuild.currentResult}"
        }
    }



}