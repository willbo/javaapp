pipeline {
    agent any
    
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }

    stages {
        stage('Build') {
            steps {
                echo "Building the application for ${params.PERSON} ..."
            }
        }
        
        stage('Dev') {
            steps {
                echo "Deploying to a dev environment ${params.PASSWORD} ..."
            }
        }
        
        stage('Test') {
            steps {
                echo 'Deploying to a test environment ...'
            }
        }
        
        stage('Prod') {
            input {
              message 'Is it OK to continue?'
              ok 'Yes, let\'s do it'
              submitter 'admin,christian'
              parameters {
                string defaultValue: 'Christian', description: 'Can I proceed?', name: 'USER', trim: false
              }
            }

            steps {
                echo 'Deploying to a prod environment ...'
            }
        }
    }
    
    options {
        quietPeriod 1
        buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '5', numToKeepStr: '3')
    }
    
    post {
      always {
        echo "This is going to run always"
      }
      unstable {
        echo "This is going to run when unstable"
      }
      aborted {
        echo "This is going to run when aborted"
      }
      failure {
        echo "This is going to run when fails"
      }
    }
}
