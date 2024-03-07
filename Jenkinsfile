pipeline {
    agent any
    parameters {
        choice(name: 'gitBranches', choices: ['main', 'b1' , 'startMockito'], description: 'Select  Git branch')
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: "${params.gitBranches}", url: 'https://github.com/Samra-iths/Jenkins_trailer.git'
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
            }
 
            post {
                always {
                    jacoco(
                    execPattern: 'target/*.exec',
                    classPattern: 'target/classes',
                    sourcePattern:'src/main/java',
                    exclusionPattern: 'src/test*')
                    junit '**/TEST*.xml'
                }
            }
        }
        
    }
}