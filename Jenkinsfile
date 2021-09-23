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
    def jenkinsPath = ''
    def nodeName = ''
    def nodesReady = ''
    def urlJenkins0 = "/8080"
    def urlJenkins1 = url0 + virtM1 + urlJenkins0
    def urlJenkins2 = url0 + virtM2 + urlJenkins0
    
pipeline{
       agent any
       //options {
           //timeout(time: 1, unit: 'SECONDS')
       //} 

    stages{
        
        stage('build'){
            steps{ 
                echo "building the app"  
                //sh "python3 ./app.py"
                }
            }
      node('MasterNode'){
        stage('Test1'){
          
            steps{
                //timeout(time: 1, unit:'MINUTES'){
                    script{ 
                        echo 'testing backup1 before starting'
                        status = sh(script:"curl -X POST -i -u admin:admin $url1", returnStatus: true)  
                    }
                //} 
            } 
          }
         
      //node('MasterNode'){
        stage('Test2'){  
            steps{
                sh "echo $status"
                    script{
                        if (status != 200 && status != 201) {  
                            sh "vagrant init"
                            sh "vagrant destroy $backup1"
                            sh "vagrant reload"
                        } else {
                            echo 'backup1 is up'
                        } 
                    }

                }
            } 
        //}             
        
        stage('Test3'){
          //node('MasterNode'){
            steps{
                script{ 
                    echo 'testing backup2 before starting'
                    status = sh(script:"curl -X POST -i -u admin:admin $url3", returnStatus: true)
                }
            } 
          //} 
        } 

        stage('Test4'){ 
          //node('MasterNode'){     
            steps{
                sh "echo $status"
                    script{
                        if (status != 200 && status != 201) {   
                            sh "vagrant init"
                            sh "vagrant destroy $backup2"
                            sh "vagrant reload $backup2"
                        } else {
                            echo 'backup2 is up'
                        } 
                }
            }
          } 
        }             
      node('BackupNode'){ 
        stage('Test5'){
            
                steps{
                    script{
                         echo 'Testing Master node IP before starting'
                         status = sh(script:"curl -X POST -i -u admin:admin $virtM2", returnStatus: true)

                    }    
                } 
            }
    }  
      node('BackupNode'){    
        stage('Test6'){ 
               
            steps{
                sh "echo $status"
                    script{
                        if (status != 200 && status != 201) {   
                            sh "vagrant init"
                            sh "vagrant destroy $virtM2"
                            sh "vagrant reload $virtM2"       
                        } else {
                            echo 'backup1 is up'
                        } 
                    }
                }
            } 
        }  
      node('MasterNode'){           
         stage('Test7'){
                steps{
                    script{
                        //status = 200
                    echo 'Testing Jenkins in Master node'
                        //timeout(time: 1, unit:'MINUTES'){
                            status = sh(script:"curl -X POST -i -u admin:admin $urlJenkins2 ", returnStatus: true)
                       //}            
                    } 
                } 
            } 
                                
         stage('Test8'){      
            steps{
                sh "echo $status"
                    script{
                        if (status != 200 && status != 201) {   
                            echo 'Jenkins must be restarted'      
                        } else {
                            echo 'Jenkins service running port:8080'
                    }
                }
            }
          }  
        }               

        stage('Test9'){ 
            steps {
                echo'testing if all the nodes are up'
                script {
                    sh(JSONPATH='{range .items[*]}{@.metadata.name}:{range @.status.conditions[*]}{@.type}={@.status};{end}{end}')
                    nodesReady = sh "kubectl get nodes -o jsonpath="$JSONPATH""
                    sh"echo $nodesReady > file2.txt)"
                    sh "grep 'Ready=True' file2.txt"
                    sh"cat file2.txt"
                } 
            }          
        }       
    }
}   