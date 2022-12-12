    kubectl create namespace limit                                                          # create namespace 'limit'
    kubectl run resource-checker --image=httpd:alpine -oyaml --dry-run=client > pod.yaml    # create pod yaml
    kubectl get pods -l app=fluentd -o wide                                                 # show pods matching label 'app=fluentd'
    kubectl get nodes -o custom-columns=NAME:.metadata.name,TAINTS:.spec.taints             # show node with formatted output
    
    kubectl create deployment random-logger --image=chentex/random-logger   # create deployment
    kubectl scale deployment/random-logger --replicas=3                     # scale deployment
    
    kubectl get pod bar --show-labels   # show pods with labels
    kubectl label pods bar color=red    # add label 'color=red' to pod bar
    kubectl label pods bar color-       # remove label 'color'
  
    kubectl cp $HOME/config.txt kuard:/tmp/config.txt   # copy file into pod
    kubectl exec kuard -- date; ll                      # run command in pod
    kubectl exec -it kuard -- sh                        # get interactive session in pod
    kubectl port-forward kuard 8080:8080                # port-forward to access via localhost
    
    kubectl get events      # show events
    
## configmaps

    kubectl create configmap mountains --from-literal=aKey=aValue --from-literal=14ers=www.14ers.com
    
    
    cat <<EOF | kubectl apply -f -
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: ucs-info
      namespace: default
    data:
      property.1: hello
      property.2: world
      ucs-org: |-
        description="Our scientists and engineers develop and implement innovative, practical solutions to some of our planet's most pressing problems"
        formation=1969
        headquarters="Cambridge, Massachusetts, US"
        membership="over 200,000"
        director="Kathleen Rest"
        president="Kenneth Kimmell"
        founder="Kurt Gottfried"
        concerns="Global warming and developing sustainable ways to feed, power, and transport ourselves, to fighting misinformation, advancing racial equity, and reducing the threat of nuclear war."
        website="ucsusa.org"
    EOF

## secrets

    kubectl create secret generic db-password --from-literal=password=MyDbPassw0rd
    kubectl get secret db-password
    kubectl get secret db-password -o yaml  # show secret with encrypted values
    kubectl get secrets db-password -o 'go-template={{index .data "password"}}' | base64 --decode  # show decrypted value 'password'
    kubectl create secret generic db-password --from-literal=password=MyDbPassw0rd --dry-run -o yaml > my-secret.yaml

## plugins 

    kubectl krew install neat   # install neat to filter our cluttering fields
    kubectl get deployments kuard -o yaml > kuard-deployment-dump.yaml # create manifest from running deployment object
    kubectl neat -f kuard-deployment-dump.yaml > kuard-deployment.yaml # destill deployment manifest to its configuration essentials


## others

    kubectl run curl-test --image=radial/busyboxplus:curl -i --tty --rm     # Start and enter a Busybox container in a separate Pod in the same Namespace
