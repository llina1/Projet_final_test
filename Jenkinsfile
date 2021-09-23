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

        stage('Test1'){
            //status = 200
            steps{
                script{ 
                echo 'testing backup1 before starting'
                status = sh(script:"curl -X POST -i -u admin:admin $url1", returnStatus: true)  
                }
            } 
        } 

        stage('Test2'){ 
          //node('master'){      
            steps{
                sh "echo $status"
                    script{
                        if (status != 200 && status != 201) {  
                            sh "vagrant init"
                            sh "vagrant destroy $backup1"
                            sh "vagrant reload"
                        }
                    }
            }
        }             
        
        stage('Test3'){
          //node('master'){
            steps{
                script{ 
                    echo 'testing backup2 before starting'
                    status = sh(script:"curl -X POST -i -u admin:admin $url3", returnStatus: true)

                }
            } 
        } 

        stage('Test4'){      
            steps{
                sh "echo $status"
                    script{
                        if (status != 200 && status != 201) {   
                            sh "vagrant init"
                            sh "vagrant destroy $backup2"
                            sh "vagrant reload $backup2"
                        }
                }
            }
        }             
        
        stage('Test5'){
            //node('master backup){ 
                //status = 200
                steps{
                    script{
                         echo 'Testing if Master node IP before starting'
                         status = sh(script:"curl -X POST -i -u admin:admin $virtM2", returnStatus: true) 

                    }    
                } 
            //} 
        }     
        stage('Test6'){ 
          //node('master backup')     
            steps{
                sh "echo $status"
                    script{
                        if (status != 200 && status != 201) {   
                            sh "vagrant init"
                            sh "vagrant destroy $virtM2"
                            sh "vagrant reload $virtM2"       
                        }
                    }
                }
        }             
         stage('Test7'){
            //node('master'){ 
                steps{
                    script{
                        //status = 200
                    echo 'Testing Jenkins in Master node'
                    //jenkinsPath = sh"whereis jenkins"
                    status = sh(script:"curl -X POST -i -u admin:admin $urlJenkins2 ", returnStatus: true)
                    } 
                } 
            //} 
        }                        
         stage('Test8'){ 
          //node('master')     
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

       /*** stage('testing'){ 
            steps {
                echo'testing if all nodes are up'
                script {
                    sh(JSONPATH='{range .items[*]}{@.metadata.name}:{range @.status.conditions[*]}{@.type}={@.status};{end}{end}')
                    nodesReady = sh(script: kubectl get nodes -o jsonpath="$JSONPATH" | grep "Ready=True")
                      sh"echo $nodesReady > file2.txt)"
                      nodesReadyVar = sh"grep "jenkins$" file1.txt"

                } 
            }          

        } /***/        
    }
}

                
            
         
    


