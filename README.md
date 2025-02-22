# aws-credentials

Get AWS credentials in various ways.

## Installation

1. Add the dependency to your `shard.yml`:

```yaml
dependencies:
  aws-credentials:
    github: y2k2mt/aws-credentials
    version: 0.1.1
```

2. Run `shards install`

## Usage

`Providers` resolves credentials in order from given` Provider`.
In the example below, at first ,`Providers` resolves credentials from EnvProvider ('AWS_ACCESS_KEY_ID' and 'AWS_SECRET_ACCESS_KEY') and then resolves credentials from SharedCredentialFileProvider ('~/.aws/credentials').

```crystal
require "aws-credentials"

include Aws::Credentials

provider = Providers.new ([
  EnvProvider.new,
  SharedCredentialFileProvider.new
] of Provider)

credentials = provider.credentials
# Aws::Credentials::Credentials(@access_key_id="AKIA...",@expiration=nil,@secret_access_key="mVlf...",@session_token=nil)
```

Current `Provider` implementations are:
- [EnvProvider](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-envvars.html)
- [SharedCredentialFileProvider](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html)
- [InstanceMetadataProvider](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-metadata.html)
- [ContainerCredentialProvider](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task-iam-roles.html)

## Contributing

1. Fork it (<https://github.com/y2k2mt/aws-credentials/fork>)
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request

## Contributors

- [y2k2mt](https://github.com/y2k2mt) - creator and maintainer
