# jenkins-vault-azure-pipeline

## Vault

- Vault instance `http://127.0.0.1:8200` running with Approle authentication and Azure Secrets Engine enabled

## Jenkins Job

- [Vault Plugin installed](https://plugins.jenkins.io/hashicorp-vault-plugin/)

- Jenkins Vault AppRole credentials added to Global credentials

- String parameter added to the job for the tenant_id value

## Jenkins Pipeline

- Login to Vault using AppRole authentication then retrieve Vault Azure Secrets Engine credentials and log into Azure

- List Azure Resource Groups

- Azure log out