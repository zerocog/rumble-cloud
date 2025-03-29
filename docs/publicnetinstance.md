# Rumble Cloud Public Network Instance

## Disclaimer

The following provides guidance for informational purposes only for standing
up a **live** public web service. Before proceeding, be warned, that what
is published can be seen by anyone with INTERNET access.

## Minimum Requirements

Complete the initial instructions given for the
[Rumble Cloud ssh commands and setup](./sshkeyspem.md)

Navigate to your Rumble cloud project and Open your cloud project. When you see from Rumble Cloud, it is assumed
you understand the navigation.

## Create Network Security Groups

TCP PROTOCOL

1. Select `Network -> Security Groups -> Create Security Group`
2. Enter a name into `Name:` field that help you remember tcp protocol
3. Select `OK`
4. Navigate to `Action` on the right for the rule in the security group you just created.
5. Select `Settings -> Create Rule`
6. Select Protocol `SSH` to specify common SSH settings (TCP on port 22)
7. Select Direction `Ingress`
8. Ether Type `IPv4` unless you want IPv6
9. Create the rule

## Create Virtual Machine Instance [^1]

### Basic Config

1. Select `Compute -> Instances -> Create Instance`, goes to `(1) Basic Config`
2. Name: Enter a name to identify the instance
3. Availability: Select `us-east-2` likely the availability zone you are on
4. Specification: Select `Compute Optimized -> c2a.large`
5. Start Source: Select `Image`
6. Operating System: `Ubuntu-24.04` is the newest as of March 2025
7. System Disk: Select `Flash_Premium` set system disk size 10+ GiB
8. System Disk: Check `Deleted with the instance`

### Network Config

Allows for instance access from your local machine over the INTERNET

1. Select `(2) Network Config`
2. Select the `Public Networks` tab, then select `PublicEphemeral` for networks
3. Subnets: Select `Automatically Assigned Address` for the network
4. Security Group: Select security group you created in TCP PROTOCOL

### System Config

1. Select `(3) System Config`
2. Login: Select  `Keypair` and choose pair that has been created before
3. Review: Select `Confirm Config` virtual machine summary for review
4. Review: Select `Confirm` and the instance is created and activated

## Load Balancers

[Using Load Balancers to provide Port Based Destination NAT](./lbport.pdf) PDF

1. You need ssh/tcp access for shell access, specify your own port for tcp 22
2. Select `Network->Load Balancers->Create Listener`
3. Specify portnum for TCP
4. Name: a name the that helps you know what port your are accessing
5. Description: any helpful details
6. Protocol: `TCP`
7. Port: `11000` or some large number is wise
8. Connection Limit: `-1` is unlimited. Pick a limit
9. You need 80/443 http access for a web server

## Access to Virtual Machine

1. ssh -i /pathto/yourcreated.pem -p PORTNUM ubuntu@<FIXED_IP_ADDRESS_FROM_INSTANCE>
2. where the IP is your Load Balancer's `Floating IP`
3. where **PORTNUM** is important relation with your load balancer configuration.
4. Select `Load Balancers --> ID/Name`
5. View `Port` for your ssh-server

## More help

Rumble Cloud documentation provides many guides. Recommend learning more at
[Rumble How To](https://docs.rumble.cloud/how_to/index.html)

Consulting services are available from [Glen CARL](http://www.buonvia.com/mobile/BVabout/)

[^1]: Ref [Rumble Create a virtual machine on a public network](
https://docs.rumble.cloud/how_to/compute/create_a_vm_on_a_public_network.html)
