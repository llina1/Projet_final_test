    def branchName=env.BRANCH_NAME 
    def status = 0
    def backup1 = "http://72.16.254.251"
    def master1 = "http://72.16.254.252"
    def backup2 = "http://72.16.254.253"
    def master2 = "http://72.16.254.254"
pipeline{
    agent any
    stages{
        stage('build'){
            steps{
                echo 'building the app'
                sh "python3 ./app.py"
                }
            }
        } 

        /***stage ('testing'){
            steps{
                echo 'testing node master before lauching'
                node('master')
                status = sh returnStdout: true, script: 'curl -X POST -i -u admin:admin $backup1'
                if (status != 200 && status != 201) {
    error("Returned status code = $response when calling $url1")
    
    vagrant destroy []  

            } 
        }   
        stage('testing'){
            echo 'Testing Jenkins in node master'
            steps{
                node('master'){
                status= sh jennkins --version
            } 

            } 
            
        } 



        stage('testing'){ 
            echo 'testing running node'
            steps{ 
                node('master'){
                    status = sh returnStdout: true, script: 'curl -X POST -i -u admin:admin $url'

if (status != 200 && status != 201) {
    error("Returned status code = $status when calling $url1")
    node ('master') { 
    git branch: 'master' , url: 'https://github.com/llina1/Projet_final_test.git'
   sh "mkdir roles"
   sh "ansible-galaxy install --roles -r requirements.yml"
    ansiblePlaybook (
    colorized: true,
    playbook:" <nom du fichier .yml>",
    hostKeyChecking: false,
    //inventory: "<chemin du fichier dans git>"
    )
}                   
}
                } 
            

            } 
        }   
    } 


        stage('testing')
         echo'testing current node running'
         steps {
        timeout(time: 5, unit: 'SECONDS') {
        node('${env.NODE_NAME}') {
            echo 'Node is up. Performing optional step.'       
        }
    }
    node('${env.NODE_NAME}') {
        echo 'This is an optional step.'
    }
} catch (e) {
    echo 'Time out on optional step. Node down?'
    node ('${env.NODE_NAME}') { 
    git branch: 'master' , url: 'https://github.com/llina1/Projet_final_test.git'
   
    sh "mkdir roles"
    sh "ansible-galaxy install --roles -r requirements.yml"
    ansiblePlaybook (
    colorized: true,
    playbook:" <nom du fichier .yml>",
    hostKeyCkecking: false
    //inventory: "<chemin du fichier dans git ex:"env/${branchName}/hosts)>",
    )
        }/***/                  
    }   
}  
                
            
         
    


