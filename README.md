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

## Stacks



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