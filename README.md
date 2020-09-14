<div align="center">
    <img src="./%40doc/figures/binbash-logo.png" 
    alt="binbash" width="250"/>
</div>
<div align="right">
  <img src="./%40doc/figures/binbash-leverage-ansible-logo.png"
  alt="leverage" width="130"/>
</div>

# Ansible Role: Binbash Certbot

Installs and configures Certbot for generating Let's Encrypt certificates.

## IMPORTANT
* It uses certbot (https://certbot.eff.org/instructions)
* Through ACME DNS-01 challenges (https://letsencrypt.org/docs/challenge-types/)
* It is expected to work with following setup:
  * An EC2 instance
  * Running nginx as a reverse proxy that terminates TLS...
  * ...and proxy passes to an upstream service (e.g. Jenkins, Prometheus, Kibana, etc)
* It handles the DNS challenge record automatically but at the moment only works with *AWS Route 53*
* At the moment it only supports *nginx*

## Requirements
1- The EC2 instance profile must have the following permissions on AWS Route 53
```
{
    "Version": "2012-10-17",
    "Id": "certbot-dns-route53 sample policy",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "route53:ListHostedZones"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect" : "Allow",
            "Action" : [
                "route53:ChangeResourceRecordSets",
                "route53:GetChange"
            ],
            "Resource" : [
                "arn:aws:route53:::hostedzone/YOURHOSTEDZONEID"
            ]
        }
    ]
}
```

# Release Management
### CircleCi PR auto-release job

<div align="left">
  <img src="./%40doc/figures/circleci-logo.png" alt="circleci" width="130"/>
</div>

- [**pipeline-job**](https://app.circleci.com/pipelines/github/binbashar/ansible-role-certbot) (**NOTE:** Will only run after merged PR)
- [**releases**](https://github.com/binbashar/ansible-role-certbot/releases) 
- [**changelog**](https://github.com/binbashar/ansible-role-certbot/blob/master/CHANGELOG.md) 


