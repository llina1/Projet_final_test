    def backup1 = "172.16.254.251"
    def virtM1 = "172.16.254.252"
    def backup2 = "172.16.254.253"
    def virtM2 = "172.16.254.254"
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
                sh"cat Vagrantfile" 
                sh"vagrant up"
                }
            }
        stage('Test1 : Bachup1'){
          //agent {label'MasterNode'}
            steps{
            //script{ 
            //try{ 
                //timeout(time: 1, unit:'MINUTES'){
                    script{ 
                        echo 'testing backup1 before starting'
                        status = sh(script:"curl -X POST -i -u admin:admin http://192.168.15.10", returnStatus: true)  
                    }
                } 
            //} catch(err) { 
                
            //} 
           // } 
        } 
        //} 

        stage('Test2: Vagrant'){ 
          //node('MasterNode'){      
            steps{
                sh "echo $status"
                    script{
                        if (status != 200 && status != 0) {  
                            //sh "vagrant init"
                            sh "vagrant destroy node1"
                            sh "vagrant reload"
                            echo "error"
                        } else {
                            echo 'backup1 is up'
                        } 
                    }

                }
            //} 
        }             
        
        stage('Test3: Backup2'){
          //node('MasterNode'){
            steps{
                script{ 
                    echo 'testing backup2 before starting'
                    status = sh(script:"curl -X POST -i -u admin:admin http://127.0.0.1:3000", returnStatus: true)
                }
            } 
          //} 
        } 

        stage('Test4: vagrant'){ 
          //node('MasterNode'){     
            steps{
                sh "echo $status"
                    script{
                        if (status != 200 && status != 0) {   
                            //sh "vagrant init"
                            //sh "vagrant destroy $backup2"
                            //sh "vagrant reload $backup2"
                        } else {
                            echo 'backup2 is up'
                        } 
                }
            }
          //} 
        }             
        
        stage('Test5: Node master'){
            //node('BackupNode'){ 
                steps{
                    script{
                         echo 'Testing Master node IP before starting'
                         status = sh(script:"curl -X POST -i -u admin:admin http://127.0.0.1:3000", returnStatus: true)

                    }    
                } 
            //} 
        }     
        stage('Test6: vagrant'){ 
          //node('BackupNode')     
            steps{
                sh "echo $status"
                    script{
                        if (status != 200 && status != 0) {   
                            //sh "vagrant init"
                            //sh "vagrant destroy $virtM2"
                            //sh "vagrant reload $virtM2"       
                        } else {
                            echo 'backup1 is up'
                        } 
                    }
                }
        }             
         stage('Test7 : Jenkins master node'){
            //node('MasterNode'){ 
                steps{
                    script{
                        //status = 200
                    echo 'Testing Jenkins in Master node'
                        //timeout(time: 1, unit:'MINUTES'){
                            status = sh(script:"curl -X POST -i -u admin:admin  http://127.0.0.1:8080", returnStatus: true)
                       //}            
                    } 
                } 
            //} 
        }                        
         stage('Test8: Jenkins response'){ 
          //node('MasterNode'){     
            steps{
                sh "echo $status"
                    script{
                        if (status != 200 && status != 0) {   
                            echo 'Jenkins must be restarted'      
                        } else {
                            echo 'Jenkins service running port:8080'
                    }
                }
            }
          //}  
        }               

        /***stage('Test9'){ 
            steps {
                echo'testing if all nodes are up'
                script {
                    sh(JSONPATH='{range .items[*]}{@.metadata.name}:{range @.status.conditions[*]}{@.type}={@.status};{end}{end}')
                    nodesReady = sh "kubectl get nodes -o jsonpath="$JSONPATH""
                    sh"echo $nodesReady > file2.txt)"
                    sh "grep 'Ready=True' file2.txt"
                    sh"cat file2.txt"
                } 
            }          
        } /***/       
    }
}   