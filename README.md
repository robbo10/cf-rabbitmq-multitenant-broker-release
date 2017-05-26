# Cloud Foundry RabbitMQ Broker

This repository contains the release for a multi-tenant RabbitMQ service broker
for Cloud Foundry. It's deployable by BOSH in the usual way.

## Updating

Clone the repository and run `./scripts/update-release` to update submodules and install dependencies.

## Deploying

Once you have a [BOSH Lite up and running locally](https://github.com/cloudfoundry/bosh-lite), run `scripts/deploy-bosh-lite`.

To deploy the release into BOSH you will need a deployment manifest. You can generate a deployment manifest using the following command:
```sh
bosh interpolate \
  --vars-file=manifests/lite-vars-file.yml \
  --var=director-uuid=$(bosh status --uuid) \
  manifests/cf-rabbitmq-broker-template.yml > manifests/cf-rabbitmq-broker.yml
```

## Testing

To run all the tests do `bundle exec rake spec`.

Use `rspec` to run a specific test:
`bundle exec rspec spec/system/syslog_forwarding_spec.rb`

### Unit Tests

To run only unit tests locally, run: `bundle exec rake spec:unit`.

### Integration Tests
To run integration tests, run: `bundle exec rake spec:integration`.
In order to be able to run the tests locally, you need to have the following
environment variables correctly configured:

```bash
export PAPERTRAIL_TOKEN=
export PAPERTRAIL_GROUP_ID=

export DEPLOYMENT_NAME=cf-rabbitmq-broker

export BOSH_DIRECTOR_URL=https://<director_username>:<director_password>@<director_ip_address_or_domain>:25555
export BOSH_MANIFEST=<path to the bosh manifest you will use in the tests>
export BOSH_TARGET=https://<director_ip_address_or_domain>:25555
export BOSH_USERNAME=<director_username>
export BOSH_PASSWORD=<director_password>

export CF_API=
export CF_DOMAIN=
export CF_USERNAME=
export CF_PASSWORD=
```
