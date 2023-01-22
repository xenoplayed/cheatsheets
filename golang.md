    go run .                    # run code
    go mod init example/hello   # create module, enable dependency tracking
    go mod tidy                 # add module as a requirement, as well as a go.sum file


    message := fmt.Sprintf("Hi, %v. Welcome!", name)    # declares and initializes variable in one line
