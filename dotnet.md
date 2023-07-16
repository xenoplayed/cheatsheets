
# dotnet CLI
Basic commands

```bash
# Manage solution / project
dotnet new sln                          # create solution 
dotnet new classlib -o library          # create library
dotnet sln add library/library.csproj   # add file to solution

# build/run code
dotnet watch run
dotnet build --configuration Release
dotnet run --configuration Release --no-build --project Tailspin.SpaceGame.Web
```

## Packages with examples

```bash
dotnet add library package Newtonsoft.Json

# install dotnet entitfy framework (preview)
dotnet tool install --global dotnet-ef --version 5.0.0-rc.1.20451.13 

# add packages
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
dotnet add package Microsoft.EntityFrameworkCore.InMemory

# Add packages for scaffolding
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet add package Microsoft.EntityFrameworkCore.Design

# Installs the scaffolding engine (dotnet-aspnet-codegenerator)
dotnet tool install -g dotnet-aspnet-codegenerator
dotnet tool update -g dotnet-aspnet-codegenerator

#Scaffolds the TodoItemsController
dotnet aspnet-codegenerator controller -name TodoItemsController -async -api -m TodoItem -dc TodoContext -outDir Controllers 
```

## manage dev certificate

If you see an error in your browser that's related to a privacy or certificate error

    dotnet dev-certs https --trust

If you're running dotnet in a vscode devcontainer, then `dotnet dev-certs https --trust` will not trust the certificate on the host.
In this case create and export the dev certs on the host and import the cert in the devcontainer:

On your host (e.g. macOS):

    dotnet dev-certs https --clean
    dotnet dev-certs https -ep certs/mycert.pfx --trust -p mycertpassword

In the devcontainer (e.g. linux)

    dotnet dev-certs https --clean --import certs/mycert.pfx -p mycertpassword

show dotnet dev-certs

    ls -la ~/.dotnet/corefx/cryptography/x509stores/my/
