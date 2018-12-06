# hut6/secrets

A nicer way to keep our secrets.

## Setup

You'll need the 1Password CLI client `op` for push/pull and the `jq` binary for extracting the UUID from responses.

```
brew cask install 1password-cli && brew install jq
```

## Usage

You'll need to create a production .env file for example.


### Starting
The first time you need a new production secret, you should create the file
and push it.
```
composer req --dev hut6/secrets
echo "DATABASE_URL=mysql://user:password@localhost/name" > .env
vendor/bin/secret-push .env # Creates `repository-name/.env` file in 1P
```

### Updating
After you make changes to production secrets file, you should push them.
```
# Update .env file...
vendor/bin/secret-push .env
```

### Refreshing
Other developers can update their production secrets like this. You
should do this before every production deployment, or include it in your
deploy script.
```
vendor/bin/secret-pull .env
```
