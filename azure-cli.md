az locations

    az account list-locations
    az account list-locations -o table
    az account list-locations --query "[].{DisplayName:displayName, Name:name}" -o table
    az account list-locations --query "sort_by([].{DisplayName:displayName, Name:name}, &DisplayName)" --output table

az appservice plans

    az appservice plan list
    az appservice plan create --name tailspin-space-game-asp --resource-group tailspin-space-game-rg --sku B1

az webapp

    webappsuffix=$RANDOM
    az webapp create --name tailspin-space-game-web-dev-$webappsuffix --resource-group tailspin-space-game-rg --plan tailspin-space-game-asp
    az webapp create --name tailspin-space-game-web-test-$webappsuffix --resource-group tailspin-space-game-rg --plan tailspin-space-game-asp
    az webapp create --name tailspin-space-game-web-staging-$webappsuffix --resource-group tailspin-space-game-rg --plan tailspin-space-game-asp
    az webapp list
    az webapp list --resource-group tailspin-space-game-rg --query "[].{hostName: defaultHostName, state: state}" --output table
    az webapp config connection-string set --name tailspin-space-game-web-dev-$webappsuffix --resource-group tailspin-space-game-rg --settings "DefaultConnection=$DB_CONNECTION_STRING" --connection-string-type SQLAzure
    az webapp config connection-string set --name tailspin-space-game-web-test-$webappsuffix --resource-group tailspin-space-game-rg --settings "DefaultConnection=$DB_CONNECTION_STRING" --connection-string-type SQLAzure
    az webapp config connection-string set --name tailspin-space-game-web-staging-$webappsuffix --resource-group tailspin-space-game-rg --settings "DefaultConnection=$DB_CONNECTION_STRING" --connection-string-type SQLAzure

pipelines

Delete all jobs in given pipeline ID with status "notStarted"
```bash
#!/bin/bash
for build_id in $(az pipelines build list --status notStarted --definition-ids 3585 --query "[].id" -o tsv); do
    az pipelines build cancel --build-id $build_id
done
```
