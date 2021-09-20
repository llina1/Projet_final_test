    def branchName=env.BRANCH_NAME
    def test_node = false
    def node_name = "${NODE_NAME}" 

    try {
    timeout(time: 5, unit: 'SECONDS') {
        node('node_name') {
            echo 'Node is up. Performing optional step.'       
        }
    }
    node('node_name') {
        echo 'This is an optional step.'
    }
} catch (e) {
    echo 'Time out on optional step. Node down?'
    node { 
    git branch: 'master' , url: 'https://github.com/llina1/Projet_final_test.git'
    //sh "mkdir roles"
    //sh "ansible-galaxy install --roles -r requirements.yml"
    //ansiblePlaybook (
    //colorized: true,
    //playbook:" <nom du fichier .yml>",
    //hostKeyCkecking: false
    //inventory: "<chemin du fichier dans git ex:"env/${branchName}/hosts)>",
   
}                //)   
}



















    pipeline {
        agent any
        stages {
            stage("build") {
                steps {
                echo'Building the application'
                sh "python3 ./app.py"
                }
            }     
        }  
    } 

