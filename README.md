# chainops

<!-- `docker build -t latest-collator -f collator.Dockerfile  ../t3rn` -->

Core chain infrastructure essential for our network:
  + collators **_IN_PROGRESS_**
  + executors **PENDING**
  + rangers   **PENDING**

## How It Works

All related infrastructure components are defined as code in the form of CloudFormation templates.

Deployments are automated and executed within Github Actions according to the respective environment:

| trigger | repo     | branch | AWS account             | Deployment identity |
|---------|----------|--------|-------------------------|---------------------|
| push    | chainops | test   | aws-test#946915630111   | aws-test-cd-runner  |
| push    | chainops | main   | aws-prod#715320985461   | aws-prod-cd-runner  |
| tag     | t3rn     |   -    | aws-prod#715320985461   | aws-prod-cd-runner  |

## Configuration

The primary configuration touchpoint is intended to be the Github Actions environment. Therefore, all stack parameters are initialized as env vars in the `env` block of [the `cd` workflow](.github/workflows/cd.yml) and should ideally be tweaked there.

Secret parameters should be set as GitHub repo secrets, currently the required secrets are:

+ AWS_ACCESS_KEY_ID_PROD
+ AWS_SECRET_ACCESS_KEY_PROD
+ AWS_ACCESS_KEY_ID_TEST
+ AWS_SECRET_ACCESS_KEY_TEST
+ DOCKERHUB_USERNAME
+ DOCKERHUB_TOKEN
+ GITHUB_PERSONAL_ACCESS_TOKEN
+ SSH_PUBLIC_KEY #TODO one key 4 each collator

The security credentials are the ones of the aws-test-cd-runner/aws-prod-cd-runner deployment identity respectively.

## Stacks

All infrastructure resources are logically grouped into separate stacks enabling a modular and layered architecture.

### `core-network-stack`

Core cloud networking resources that are globally shared within the engineering organizational unit.

**Parameters** None

**Exports**

+ VpcId
+ NetworkLoadBalancerArn
+ PrivateSubnet1Id
+ PrivateSubnet2Id
+ PublicSubnet1Id
+ PublicSubnet2Id

### `collator-setup-stack` #TODO

**Parameters** None

...

**Exports**

+ ...

### `collator-network-stack`

Collator cloud networking resources.

**Parameters**

+ RelaychainNodeP2pPort
+ CollatorP2pPort
+ CollatorHttpPort
+ CollatorWsPort

**Exports**

+ CollatorTargetGroupArn
+ CollatorSecurityGroupId
+ MountTargetSecurityGroupId

### `collator-storage-stack` #TODO

### `collator-core-stack` #TODO

### `collator-monitoring-stack` #TODO