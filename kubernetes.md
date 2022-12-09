    kubectl create namespace limit                                                          # create namespace 'limit'
    kubectl run resource-checker --image=httpd:alpine -oyaml --dry-run=client > pod.yaml    # create pod yaml
  
  
