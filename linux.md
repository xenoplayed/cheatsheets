### replace string in file

    sed -i 's/127.0.0.1/naboo-cp/g' ~/.kube/k3s-pi.kube.config  # linux
    sed -i '.original' -e 's/127.0.0.1/naboo-cp/g' ~/.kube/k3s-pi.kube.config  # macOS (-i needs value to create backup file, in this example 'k3s-pi.kube.config.original')
    
