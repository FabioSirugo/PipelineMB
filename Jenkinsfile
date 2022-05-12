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
            when {
             branch 'master'
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
            post{
                success{
                    emailext(attachLog: true, body: 'Hotfix risolto, i test sono stati superati' , subject: 'Hotfix branch resault', to: 'fabiosirugo8@gmail.com')
                }
            }
        }
        
    }




}