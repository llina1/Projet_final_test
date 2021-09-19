try{
    def branchName=env.BRANCH_NAME
    pipeline {
        agent any
        stages {
            stage("build") {
                steps {
                echo'Building the application'

                }
            }
    


            stage("Run script") {
                steps {
                    sh "python3 ./app.py"
                }
            } 
            stage("Ansible - Deploy"){
                git branch: 'master' , url: 'https://github.com/llina1/Projet_final_test.git'
                sh "mkdir roles"
                sh "ansible-galaxy install --roles -r requirements.yml"
                ansiblePlaybook (
                    colorized: true,
                    //playbook:" <nom du fichier .yml>",
                    hostKeyCkecking: false
                    //inventory: "<chemin du fichier dans git ex:"env/${branchName}/hosts)>",

                )
            } 
        }  
    } 
}
