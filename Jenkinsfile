pipeline {
    agent any
    
    tools {
        maven 'Maven 3.6.3'
        jdk 'Java 9'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                    step([
                        $class           : 'JacocoPublisher',
                        execPattern      : '**/**.exec',
                        classPattern     : '**/classes',
                        sourcePattern    : '**/src/main/java',
                        exclusionPattern : '**/*Test.class'
                    ])
                }
            }
        }
    }
    
    post {
        always {
            archiveArtifacts artifacts: 'target/*.jar'
        }
    }
}
