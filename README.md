Launch EC2 Instance with Wireguard
==================================

This [Cloudformation](https://aws.amazon.com/cloudformation/) creates a personal [Wireguard](https://www.wireguard.com/) VPN server in AWS. I assume a cursory understanding of AWS, Cloudformation and EC2 with existing ssh key.

You will need the following:

* Launch the `wireguard-eip-master.json` template first. It will export the elastic IP used by the `wireguard-master.json`template (so you can conveniently use the same public IP).
* Your VPC's default security group ID

The default AMI is Amazon Linux 2.

Steps:

* After the cloudformation is deployed and server has rebooted as required ssh into it and start wireguard
    ```wg-quick up wg0
    ```
* Then get the client config and paste it into your client's configuration
    ```sudo cat /tmp/wg0-client.conf
    ```

Caveats

* The procecess leverages Google DNS 8.8.4.4 for name resolution. 