pipeline {
    agent any 
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