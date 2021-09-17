pipeline {
    agent any
    stages {
        stage("build") {
            steps {
                echo'Building the application'
                sh 'python app.py'

            }
        }
    


stage("Run script") {
            steps {
                sh "python ./app.py"
            }
        } 
    }  
} 