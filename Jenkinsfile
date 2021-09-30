pipeline{
		agent{
			
			kubernetes {
			    
			    yaml '''
        apiVersion: v1
        kind: Pod
        spec:
          containers:
          - name: helm
            image: alpine/helm
            command:
            - cat
            tty: true
        '''
    
    }
		}
    environment {
        MY_KUBECONFIG = credentials('config-file')
    }
		stages{
				stage('Checkout Source') {
      steps {
        git 'https://github.com/sharan-sripada/bc16-helm-jenkins.git'
      }
    }
                    
                stage("Build") {
                        steps {
                            container('helm'){
                               sh """
                                  export KUBECONFIG=\${MY_KUBECONFIG}
                                  helm install bc16 . -n bc16                              
                                  """
                            
                            }
                            
                        }
                    }
                    
                    
				
                
            }
