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
9. 
Create the rule.

## Create Virtual Machine Instance [^1]

1. Select `Compute -> Instances -> Create Instance`
2. 


## Load Balancers

[Using Load Balancers to provide Port Based Destination NAT](./lbport.pdf) PDF

## More help

Rumble Cloud documentation provides many guides. Recommend learning more at
[Rumble How To](https://docs.rumble.cloud/how_to/index.html)

Consulting services are available from [Glen CARL](http://www.buonvia.com/mobile/BVabout/)

[^1]: Ref [Rumble Create a virtual machine on a public network](
https://docs.rumble.cloud/how_to/compute/create_a_vm_on_a_public_network.html)
