# Write-up Template

### Analyze, choose, and justify the appropriate resource option for deploying the app.

*For **both** a VM or App Service solution for the CMS app:*
- *Analyze costs, scalability, availability, and workflow*
- *Choose the appropriate solution (VM or App Service) for deploying the app*
- *Justify your choice*

### Assess app changes that would change your decision.

*Detail how the app and any other needs would have to change for you to change your decision in the last section.* 


Notes While Creating

Joes-MBP:nd081-c1-provisioning-microsoft-azure-vms-project-starter-master joefried$ az sql server create --admin-user project1user --admin-password Project1password --name project-1-sql-db --resource-group Project-1 --location westus2 --enable-public-network true --verbose
Argument '--enable-public-network' is in preview. It may be changed/removed in a future release.
{- Finished ..
  "administratorLogin": "project1user",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "project-1-sql-db.database.windows.net",
  "id": "/subscriptions/c86beb26-3934-4364-85c5-ca12f97813c1/resourceGroups/Project-1/providers/Microsoft.Sql/servers/project-1-sql-db",
  "identity": null,
  "kind": "v12.0",
  "location": "westus2",
  "minimalTlsVersion": null,
  "name": "project-1-sql-db",
  "privateEndpointConnections": [],
  "publicNetworkAccess": "Enabled",
  "resourceGroup": "Project-1",
  "state": "Ready",
  "tags": null,
  "type": "Microsoft.Sql/servers",
  "version": "12.0"
}
Command ran in 47.670 seconds (init: 0.072, invoke: 47.599)

NEED TO ADD FIREWALL RULES FOR TRAFFIC WITH OUR SQL SERVER

Joes-MBP:nd081-c1-provisioning-microsoft-azure-vms-project-starter-master joefried$ az sql server firewall-rule create \
> -g Project-1 \
> -s project-1-sql-db \
> -n azureaccess \
> --start-ip-address 0.0.0.0 \
> --end-ip-address 0.0.0.0 \
> --verbose
{
  "endIpAddress": "0.0.0.0",
  "id": "/subscriptions/c86beb26-3934-4364-85c5-ca12f97813c1/resourceGroups/Project-1/providers/Microsoft.Sql/servers/project-1-sql-db/firewallRules/azureaccess",
  "kind": "v12.0",
  "location": "West US 2",
  "name": "azureaccess",
  "resourceGroup": "Project-1",
  "startIpAddress": "0.0.0.0",
  "type": "Microsoft.Sql/servers/firewallRules"
}

Joes-MBP:nd081-c1-provisioning-microsoft-azure-vms-project-starter-master joefried$ az sql db create \
> --name project-1-db \
> --resource-group Project-1 \
> --server project-1-sql-db \
> --tier Basic  \
> --verbose
{- Finished ..
  "autoPauseDelay": null,
  "backupStorageRedundancy": "Geo",
  "catalogCollation": "SQL_Latin1_General_CP1_CI_AS",
  "collation": "SQL_Latin1_General_CP1_CI_AS",
  "createMode": null,
  "creationDate": "2020-10-22T22:51:19.297000+00:00",
  "currentServiceObjectiveName": "Basic",
  "currentSku": {
    "capacity": 5,
    "family": null,
    "name": "Basic",
    "size": null,
    "tier": "Basic"
  },
  "databaseId": "7cb5c320-99b4-46af-9c38-3e63bc1f1730",
  "defaultSecondaryLocation": "westcentralus",
  "earliestRestoreDate": "2020-10-22T23:21:19.297000+00:00",
  "edition": "Basic",
  "elasticPoolId": null,
  "elasticPoolName": null,
  "failoverGroupId": null,
  "id": "/subscriptions/c86beb26-3934-4364-85c5-ca12f97813c1/resourceGroups/Project-1/providers/Microsoft.Sql/servers/project-1-sql-db/databases/project-1-db",
  "kind": "v12.0,user",
  "licenseType": null,
  "location": "westus2",
  "longTermRetentionBackupResourceId": null,
  "managedBy": null,
  "maxLogSizeBytes": null,
  "maxSizeBytes": 2147483648,
  "minCapacity": null,
  "name": "project-1-db",
  "pausedDate": null,
  "readReplicaCount": 0,
  "readScale": "Disabled",
  "recoverableDatabaseId": null,
  "recoveryServicesRecoveryPointId": null,
  "requestedServiceObjectiveName": "Basic",
  "resourceGroup": "Project-1",
  "restorableDroppedDatabaseId": null,
  "restorePointInTime": null,
  "resumedDate": null,
  "sampleName": null,
  "sku": {
    "capacity": 5,
    "family": null,
    "name": "Basic",
    "size": null,
    "tier": "Basic"
  },
  "sourceDatabaseDeletionDate": null,
  "sourceDatabaseId": null,
  "status": "Online",
  "tags": null,
  "type": "Microsoft.Sql/servers/databases",
  "zoneRedundant": false
}
Command ran in 47.828 seconds (init: 0.096, invoke: 47.732)

