Launch EC2 Instance with Wireguard
==================================

This [Cloudformation](https://aws.amazon.com/cloudformation/) creates a personal [Wireguard](https://www.wireguard.com/) VPN server in AWS. I assume a cursory understanding of AWS console and Cloudformation.

You will need the following:

* In the AWS console, launch the `wireguard-eip-master.json` template first. It will export the elastic IP used by the `wireguard-master.json`template (so you can conveniently use the same public IP).  The true/false option allows one to stand up the `wireguard-master.json` with out the export from the EIP, if undesired.
* Your VPC's default security group ID (auto-populated in Cloudformation dropdown)

Steps:

1. Download the [Wireguard client](https://www.wireguard.com/install/) for your platform
2. Log into AWS console and go to the region of preference
3. Depoly the `wireguard-eip-master.json` template (button here?)
4. Deploy the the `wireguard-master.json` template (button here?)
5. After the Cloudformation is deployed and server has rebooted click the link in the Cloudformation Outputs to see the encrypted client config in SSM Parameter Store
6. Paste config into your client and activate (or add it to your favorite, and secure, qr code generator to add a tunnel to a mobile device)
7. Profit

Of Note:

* The default AMI is Amazon Linux 2 and it grabs the latest (NOT FOR PRODUCTION)
* This leverages Cloudflare's DNS 1.1.1.1
* The client config is sent to a kms encrypted SSM Parameter Store
* There is a force reboot at the end of userdata so that Wireguard comes up gracefully
* The instance does not get an ssh key passed in and ssh port is not open
