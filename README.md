# secrets

Secret management using [vault](https://www.vaultproject.io/) and [consul](https://www.consul.io/)

    docker-compose up

## vault

To initialise vault

    docker exec -ti vault /vault/init

To add a simple secret

    docker exec -ti vault /vault/add-secret KEY VALUE

## consul

Add secret

    [secrets] curl -s -XPUT http://consul.internal:8500/v1/kv/foo --data 'bar'
    true%

Get secret

    [secrets] curl -s http://consul.internal:8500/v1/kv/foo | jq ".[0].Value" | tr -d \" | base64 --decode
    bar%
