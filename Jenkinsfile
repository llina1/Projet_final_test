pipeline {
    agent any
    stages {
        stage("build") {
            steps {
                echo'Building the application'

            }
        }
    }
}

stage('Run Program') {
    dir('sources') {
       steps {
           sh 'python3 app.py'
       }
    }
}