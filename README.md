# AWS ECS `servicesStable` waiter (with retries)

AWS provides a way to wait for certain ECS services to become `stable`, but this command times out after 10 minutes.\
This action allows you to wait for services to become stable **and** retry the waiting process as many times as you want.

## Inputs

### `ecs-cluster`

**Required** - _string_\
The ECS cluster that contains your services.

### `ecs-services`

_Optional_ - _string[]_\
A list of ECS services to make sure are stable. e.g. '["service1","service2"]'. Defaults to all services within cluster.

### `max-timeout-mins`

_Optional_ - _integer_\
The number of minutes to wait trying the stability check. Default `20`.

### `aws-access-key-id`

_Optional_ - _string_\
Your AWS ACCESS_KEY_ID.\
Must be provided as an input / defined as an environment variable.

### `aws-secret-access-key`

_Optional_ - _string_\
Your AWS SECRET_ACCESS_KEY.\
Must be provided as an input / defined as an environment variable.

### `aws-region`

_Optional_ - _string_\
Your AWS REGION.\
Must be provided as an input / defined as an environment variable.

### `verbose`

_Optional_ - _boolean_\
Whether to print verbose debug messages to the console. Default `false`.

## Outputs

### `retries`

_integer_\
How many retries happened until success. Each retry is at most 10 mins.

### `time-taken-secs`

_integer_\
How many seconds elapased.

## Example usage

### Using all available options

```yaml
uses: oryanmoshe/ecs-wait-action@v1.3
with:
  aws-access-key-id: AKIAIOSFODNN7EXAMPLE
  aws-secret-access-key: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
  aws-region: us-east-1
  ecs-cluster: my-ecs-cluster
  ecs-services: '["my-ecs-service-1", "my-ecs-service-2"]'
  max-timeout-mins: 15
  verbose: false
```

### Minimal configuration

```yaml
uses: oryanmoshe/ecs-wait-action@v1.3
with:
  ecs-cluster: my-ecs-cluster
```
