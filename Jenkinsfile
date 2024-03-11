pipeline {
    agent any 
    parameters {
        choice(name: 'gitBranches', choices: ['main', 'b1' , 'startMockito'], description: 'Select  Git branch')
    }
    stages {
        stage('Checkout') {
            
                 steps {
            
                    checkout([$class: 'GitSCM', branches: [[name: "${params.gitBranches}"]], userRemoteConfigs: [[url: 'https://github.com/Samra-iths/Jenkins_trailer.git']]])
                }
            
            }
      stage('Build') {
            steps {
                bat "mvn compile"
                
            }
      }
      
      stage('Test') {
            steps {
                bat "mvn test"
                bat "robot test" 
            }
 
            post {
                always {
                    jacoco(
                    execPattern: 'target/*.exec',
                    classPattern: 'target/classes',
                    sourcePattern:'src/main/java',
                    exclusionPattern: 'src/test*')
                    junit '**/TEST*.xml'
                    robot html: true, 
                    logFileName: 'output.xml', 
                    reportFileName: 'report.html'
                }
            }
        }
        
    }
}