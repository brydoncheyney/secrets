# Secrets

Secret management using [vault](https://www.vaultproject.io/) and [consul](https://www.consul.io/)

    docker-compose up

## Consul

Add a secret

    [secrets] curl -s -XPUT http://consul.internal:8500/v1/kv/foo --data 'bar'
    true%

Get secret

    [secrets] curl -s http://consul.internal:8500/v1/kv/foo | jq ".[0].Value" | tr -d \" | base64 --decode
    bar%

## Vault

To initialise vault

    docker exec -ti vault /vault/init

To add a simple secret

    docker exec -ti vault /vault/add-secret KEY VALUE

### CLI

Set up the vault environment

    export VAULT_ADDR=http://vault.internal:8200
    export VAULT_TOKEN=$(awk '/Initial Root Token/ {print $NF}' ./vault/keys)

Add a secret

    vault write secret/foo value=bar

Get secret

    vault read secret/foo

### API

Set up the vault environment

    export VAULT_TOKEN=$(awk '/Initial Root Token/ {print $NF}' ./vault/keys)

Add a secret

    curl -XPUT \
         -H "X-Vault-Token: ${VAULT_TOKEN}" \
         -H "Content-Type: application/json" \
         -d '{"value":"bar"}' \
         http://vault.internal:8200/v1/secret/foo
    true%

Get secret

    curl -XGET \
         -H "X-Vault-Token: ${VAULT_TOKEN}" \
         http://vault.internal:8200/v1/secret/foo \
       | jq ".data.value" | tr -d \"
    bar
