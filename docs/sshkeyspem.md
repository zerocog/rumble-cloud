# Rumble Cloud ssh commands and setup [^1]

The following is a supplemental document to Rumble Cloud
*SSH command line tools* [^2] with the intent to simplify the
ssh access to an instance with a load balancer configuration
for a **public** network.

## Mininum Requirements

Rumble Cloud services [^4]

1. Starter Pack
2. **Two** Floatiing IP Address

The **Starter Pack** includes one Floating IP Address, however, to provide
a public service you need a mininum of two addresses. Therefore, at a minium
it is recommended to purchase the **Stqrter Pack** and **1 Floating IP Address**

Follow the instructions at
[Rumble Get Started](https://docs.rumble.cloud/get_started/index.html)

## Navigate to Rumble Cloud project

1. [Manage cloud projects](https://docs.rumble.cloud/guides/account/manage_cloud_projects.html)
2. [portal.rumble.cloud](https://portal.rumble.cloud)
3. Select `open` for your desired organization
4. LHS, open projects and Select desired project
5. Select `Open Cloud Project`

## Key Pairs [^3]

Rumble recommends a id_ed25519 key. Reference some other best practices
from BRANDON CHECKETTS
[SSH Key Best Practices for 2025 – Using ed25519, key rotation, and other best practices](https://www.brandonchecketts.com/archives/ssh-ed25519-key-best-practices-for-2025)

```bash
cd .ssh
ssh-keygen -t ed25519
ssh-add id_ed2519
```

### Upload the public key

From Bash Terminal

1. cat ~/.ssh/id_ed25519.pub | pbcopy

From Rumble Cloud

1. Select `Compute -> Key Pairs -> Create Keypair`
2. Select `Import Keypair`
3. from your pbcopy, paste into the `Public Key` field
4. Make sure not trailing spaces for the paste
5. Select `OK`

If successful, you will see your key pair associated with your
Rumble Cloud account, and you can use the key pair across the
Rumble Cloud *projects*.

## pem creation [^3]

From Rumble Cloud

1. Select `Compute -> Key Pairs -> Create Keypair`
2. Select `Create Keypair`
3. Enter a name without extension into `Name:` field
   for example, `myexamplename`
4. Verify your browser can download from `region`.rumble.cloud
5. Select `OK`
6. Verify file `myexamplename.pem` downloads as a pem certificate

### PEM move and permissions [^3]

```bash
mv myexample.pem ~/.ssh
chmod 400 myexample.pem
cd ~/.ssh
ssh-add myexample.pem
```

### Associate PEM with instance [^3]

When you [create a virtual machine instance](./publicnetinstance.md),
you will be asked to provide a key pair. It is recommended to choose one of your pem files.

To find the pem or other keypair name associated with your instance,

1. Select `Compute --> Instances`
2. Select the `Settings` icon for instance ID/Name of interest
3. Select `Access Info`
4. View your Keypair: `Name` from your Compute / Key Pairs

## ssh calls to your load balanced instance

```bash
ssh -i ~/.ssh/myexamplename.pem -p portnum ubuntu@my_floating_ip
```

where **portnum** is important relation with your load balancer configuration.

1. Select `Load Balancers --> ID/Name`
2. View `Port` for your ssh-server

## More help

Rumble Cloud documentation provides many guides. Recommend learning more at
[Rumble How To](https://docs.rumble.cloud/how_to/index.html)

Consulting services are available from [Glen CARL](http://www.buonvia.com/mobile/BVabout/)

[^1]: This document only supports Linux based operating systems, such as MacOS and ubuntu.
[^2]: Ref [Rumble SSH Guide](https://docs.rumble.cloud/guides/tools/SSH.html)
[^3]: Ref [Rumble SSH Key Pair(https://docs.rumble.cloud/how_to/tools/add_an_SSH_key_pair.html)
[^4]: Ref [Rumble Cloud Service Pricing](https://www.rumble.cloud/pricing/) to get access
