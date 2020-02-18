# hut6/secrets

A nicer way to manage our secrets.

## Setup

You'll need the 1Password CLI client `op` for push/pull. 

## Required files & directories

You'll need to create a `/secrets` directory which will contain a `environment.env` file for each of your deployment environments, eg `production.env`, or `staging.env`

You will also need a `/hosts.yml` inventory file (as per Deployer https://deployer.org/docs/hosts.html) with an additional `secrets_uuid` value for each host.

## Install

```
composer req --dev hut6/secrets
```

## Pushing to 1Password

To push your file from the secrets directory to 1Password, run the following command.

```
bin/secrets push production
```

Replace production with the right host key, as per your hosts.yml file. 

The first time you run this command, it will ask you which vault needs to be used. 

The same command can be used to update the entry in 1password after you make changes to production secrets file.

## Pulling from 1Password

This will pull the secrets file from 1password, using the UUID specified in hosts.yml, and add it to the secrets directory. 

```
bin/secrets pull production 
```

## Updating the docker secrets 

This will load the secrets (from the secrets directory) into the docker daemon for the specified host. Containers likely will need restarting, and this command doesn't do this. 

```
bin/secrets load production 
```

