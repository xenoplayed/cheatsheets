    kubectl create namespace limit                                                          # create namespace 'limit'
    kubectl run resource-checker --image=httpd:alpine -oyaml --dry-run=client > pod.yaml    # create pod yaml
  
  
    kubectl cp $HOME/config.txt kuard:/tmp/config.txt   # copy file into pod
    kubectl exec kuard -- date; ll                      # run command in pod
    kubectl exec -it kuard -- sh                        # get interactive session in pod
    kubectl port-forward kuard 8080:8080                # port-forward to access via localhost
    
    
    
## plugins 

    kubectl krew install neat   # install neat to filter our cluttering fields
    kubectl get deployments kuard -o yaml > kuard-deployment-dump.yaml # create manifest from running deployment object
    kubectl neat -f kuard-deployment-dump.yaml > kuard-deployment.yaml # destill deployment manifest to its configuration essentials
