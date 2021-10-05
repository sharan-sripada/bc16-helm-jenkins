import groovy.transform.Field

podTemplate(label: 'bc16', containers: [
	containerTemplate(name: 'helm', image: 'alpine/helm', command: 'cat', ttyEnabled: true)],
	volumes: [hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock')]
) {

  node('bc16'){


properties([
            parameters([
                string(
                    defaultValue: 'latest',
                    description: '', 
                    name: 'fe_version',
                    trim: true),
                string(
                    defaultValue: 'latest',
                    description: '', 
                    name: 'be_version',
                    trim: true),
            ])
        ])

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
