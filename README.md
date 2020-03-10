# vault-DynamoDB
Vault HA cluster with Dynamodb

## Description
This repo contains Vagrant script to spin up a HA Vault cluster with DynamoDB as back-end. 

## Steps/procedure

1. Install Hashicorp Vagrant: https://www.vagrantup.com/docs/installation/
2. Place Vault binary in `ENT` folder where you have downloaded this repo.
3. Create DynamoDB table and make sure the table schema is like this:

```
Primary partition key: "Path", a string
Primary sort key: "Key", a string
```

detail documentation can be find here: https://www.vaultproject.io/docs/configuration/storage/dynamodb/#table-schema

4. Update `setupVaultServer.sh` and pass your DynamoDB credentials and details

```
storage "dynamodb" {
    ha_enabled="true"
  region = "us-west-2"
  table    = "vault_data"
  access_key = ${AWS_ACCESSKEY}
  secret_key = ${AWS_SECRETKEY}
}
```

5. Run ` $ Vagrant up` command to provision 2 Vault servers.
6. SSH into one of the Vault node `$ vagrant ssh vault1`
7. Initialize the Vault server `$ vault operator init`
8. You DynamoDB instance will updated with multiple mounts confirming successful installation
