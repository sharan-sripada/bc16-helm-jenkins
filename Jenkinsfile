import groovy.transform.Field

podTemplate(label: 'bc16', containers: [
	containerTemplate(name: 'helm', image: 'alpine/helm', command: 'cat', ttyEnabled: true)],
	volumes: [hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock')]
) {

  node('bc16'){

    	stage('Checkout Source') {
      
        git 'https://github.com/sharan-sripada/bc16-helm-jenkins.git'
      
    }

    
                stage("Build") {
                        
                    container('helm'){
                        withCredentials([file(credentialsId: 'config-file', variable: 'config')]) {


                               sh """
                                  export KUBECONFIG=\${config}
                                  helm upgrade --install  bc16 . -n bc16                              
                                  """
                        }    
                    }
                            
                        
                }

		
		
		}
	

    

 

}