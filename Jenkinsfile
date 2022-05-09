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
                sh 'node --version'
            }
        }
        stage('Deploy'){
            when{
                expression{
                    !("SUCCESS".equals(currentBuild.previousBuild.result))
                }
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
                echo "I'm deploying i'm in master branch"
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




}