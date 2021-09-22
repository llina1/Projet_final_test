    def backup1 = "72.16.254.251"
    def virtM1 = "72.16.254.252"
    def backup2 = "72.16.254.253"
    def virtM2 = "72.16.254.254"
    def url0 = "http://"
    def url1 = url0 + backup1
    def url2 = url0 + virtM1
    def url3 = url0+ backup2
    def url4 = url0 + virtM2
    def status = 0
    
pipeline{
       agent any
       //options {
           //timeout(time: 1, unit: 'SECONDS')
       //} 

    stages{
 
/***        stage('build'){
            steps{ 
                echo "building the app"  
                //sh "python3 ./app.py"
                }
            }

        stage('Test1'){
            steps{
                script{ 
                echo 'testing backup1 before starting'
                //int status = sh(script: curl -s -o /dev/null -w "%{http_code}" $url1)
                //def response = sh(script: 'curl $url1', returnStdout: true)
                status = sh(script:"curl -X POST -i -u admin:admin $url1", returnStatus: true)  
                }
            } 
        } 

        stage('Test3'){      
            steps{
                sh "echo $status"
                    script{
                        if (status != 200 && status != 201) {  
                        //error("Returned status code = $status when calling $url1") 
                        sh "vagrant init"
                        sh "vagrant destroy $backup1"
                        sh "vagrant reload $backup1"
                    }
                }
            }
        }             
        stage('Import'){ 
            steps{ 
                git branch: 'master' , url: 'https://github.com/llina1/Projet_final_test.git'
                sh "rmdir -r roles"
                sh "mkdir roles"
                sh "ansible-galaxy install --roles -r requirements.yml"
                ansiblePlaybook (
                colorized: true,
                playbook:" <nom du fichier .yml>",
                hostKeyChecking: false,
                inventory: "<chemin du fichier dans git>"
                )        
            }
        } 
         stage('Test3'){
            steps{
                script{ 
                echo 'testing backup1 before starting'
                //int status = sh(script: curl -s -o /dev/null -w "%{http_code}" $url1)
                //def response = sh(script: 'curl $url1', returnStdout: true)
                status = sh(script:"curl -X POST -i -u admin:admin $url3", returnStatus: true)  
                }
            } 
        } 

        stage('Test4'){      
            steps{
                sh "echo $status"
                    script{
                        if (status != 200 && status != 201) {  
                        //error("Returned status code = $status when calling $url1") 
                        sh "vagrant init"
                        sh "vagrant destroy $backup2"
                        sh "vagrant reload $backup2"
                    }
                }
            }
        }             
        stage('Import'){ 
            steps{ 
                git branch: 'master' , url: 'https://github.com/llina1/Projet_final_test.git'
                sh "rmdir -r roles"
                sh "mkdir roles"
                sh "ansible-galaxy install --roles -r requirements.yml"
                ansiblePlaybook (
                colorized: true,
                playbook:" <nom du fichier .yml>",
                hostKeyChecking: false,
                inventory: "<chemin du fichier dans git>"
                )        
            }
        }
     
  
    /***/        
           
        stage('Test3'){
            //node { 
                echo 'Testing Jenkins in Master node '
                steps{
                    jenkinsPath = sh"whereis jenkins"
                } 
            //} 
        }

        stage('Test4'){
                steps{
                    sh "echo $jenkinsPath > file.txt" 
                    script{
                        jenkinsVar = sh"grep "jenkins$""
                        if (jenkinsVar != '') {
                            echo 'jenkins is installed'
                        } else {
                            echo 'jenkins is not installed'
                        } 
                    }  
                } 

        } 
         

    } 
            
} 



    


/***
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
} 
           
    }  /***/ 
    

                
            
         
    


