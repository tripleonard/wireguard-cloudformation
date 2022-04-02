Launch EC2 Instance with Wireguard
==================================

This [Cloudformation](https://aws.amazon.com/cloudformation/) creates a personal [Wireguard](https://www.wireguard.com/) VPN server in AWS. I assume a cursory understanding of AWS console and Cloudformation.

Steps:

1. Download the [Wireguard client](https://www.wireguard.com/install/) for your platform
2. Log into AWS console and go to the region of preference
3. Depoly the `wireguard.json` template
4. After the Cloudformation is deployed and server has rebooted click the link in the Cloudformation Outputs to see the encrypted client config in SSM Parameter Store (or navigate to Parameter Store in the console)
5. Paste config into your client and activate (or add it to your favorite, and secure, qr code generator to add a tunnel to a mobile device)
6. Profit?

Of Note:

* The default AMI is Amazon Linux 2 and it grabs the latest (NOT FOR PRODUCTION)
* This leverages Cloudflare's DNS 1.1.1.1
* The client config is sent to a kms encrypted SSM Parameter Store
* There is a force reboot at the end of userdata so that Wireguard comes up gracefully
* The instance does not get an ssh key passed in and ssh port is not open
