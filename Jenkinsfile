pipeline { 
 agent any 
  stages { 
        stage("installing prerequisites") { 
        steps { 
           script { 
              sh """ 
                    sud0 amazon-linux-extras install java-openjdk11 -y 
                    sleep 5 
                    sudo yum install git maven -y  
                    sudo yum install docker -y
                    sudo sleep 5 
                    sudo usermod -aG docker $user 
                    sudo usermod -aG docker root 
                    sudo systemctl enable docker 
                    sudo systemctl start docker
                    sudo chmod 777 /var/run/docker.sock 
                    sudo sytemctl restart docker 
                    sudo docker info 
                 """  
              } 
             } 
            } 
           stage("installing SonarQube tool") { 
             steps { 
              script { 
                 sh "docker run -itd --name SonarQube -p 9000-9000 SonarQube:Its-comunit" 
              } 
            } 
          }
          stage("instlling Nexustool") { 
          steps { 
            script { 
                 sh "docker run -itd --name nexus -p 081-8081 Sonartype/nexus3" 
              } 
            } 
          } 
           stage("instlling Trivy") { 
          steps { 
            script {  
                 sh "curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sh -s -- -b /usr/local/bin v0.18.3" 
                 sh "trivy --version"
              } 
            } 
          }  
      } 
  }


            
