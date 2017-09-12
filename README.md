# secrets

Secret management using [vault](https://www.vaultproject.io/) and [consul](https://www.consul.io/)

    docker-compose up

## vault

TODO

## consul

Add secret

    [secrets] curl -s -XPUT http://consul.internal:8500/v1/kv/foo --data 'bar'
    true%

Get secret

    [secrets] curl -s http://consul.internal:8500/v1/kv/foo | jq ".[0].Value" | tr -d \" | base64 --decode
    bar%
