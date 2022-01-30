```bash
cd webapp-azsql-azcli
```

login to azcli
```bash
subscrname="visual studio enterprise subscription"
az login
az account set --subscription $subscrname
```

deploy to rg-group rg-webapp-sql
```bash
chmod +x deploy.sh
./deploy.sh
```

clean sollution
```bash
az group delete --name rg-webapp-sql
```

get connection string
```bash
serverName=$(az sql server list -o tsv --query "[? resourceGroup == 'rg-webapp-sql' ].name")
connstring=$(az sql db show-connection-string --name MySampleDatabase --server $serverName \
--client ado.net --output tsv)

username="@4dm1n1str4t0r"
sqlServerPassword="admin@123456"

connstring=${connstring//<username>/${username}}
connstring=${connstring//<password>/${sqlServerPassword}}

echo $connstring
```
