---
title: "Active Directory: Hell-bent on Kerberos"
datePublished: Tue Jan 21 2025 07:28:28 GMT+0000 (Coordinated Universal Time)
cuid: cm665lmqd000g09ic9de5bamh
slug: hell-bent-on-kerberos
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1737441148069/942fdda4-9f85-48e3-b108-1d4ea74f7bb0.png

---

## Sounds darn good

I know right? It’s equally much of a headache. Kerberos is an authentication protocol that’s made and maintained by MIT and used in numerous applications like in Windows Active Directory. Kerberos was derived from the greek word “Cerberus”.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">In Greek mythology, Cerberus, often referred to as the hound of Hades, is a multi-headed dog that guards the gates of the underworld to prevent the dead from leaving.<a target="_self" rel="noopener noreferrer nofollow" class="y171A xmq3o Q7PwXb a-no-hover-decoration" href="https://en.wikipedia.org/wiki/Cerberus" style="pointer-events: none">&nbsp;Wikipedia</a></div>
</div>

## Wait, what’s Active Directory?

### Some Basic Terms and Objects

Active Directory is a central repository that centralises administration of components of windows machines within a Domain (or a network). There’s something called Active Directory domain service, which holds info for all objects in network. What’s an object? Users, Groups, Machines, the usual deal.

types of objects include security principals (can be auth’d by domain and can be assigned perms over resources), machines (saved as &lt;machine\_name&gt;$ )

security groups: groups of security principals (also considered as security principals!), here’s a priority-wise list of security groups…

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737381591731/b531a147-6892-4695-9e4d-5edf4bf299f0.png align="center")

### Organisational units

Organisational units group users and machines with similar permission sets

1. builtin (default groups)
    
2. computers
    
3. DCs
    
4. user
    
5. managed service accounts (every resource requires a service account)
    

![Active Directory OU (Organizational Unit): Ultimate Guide – TheITBros](https://theitbros.com/wp-content/uploads/2023/09/how-to-create-ou-in-active-directory.png align="left")

Security groups are to grant permissions together, while OUs are to group objects with similar permissions. By searching about GPOs on the Windows start menu, you can set policies for multiple groups.

### Trees, Forests, Subdomaining

trees is to create subdomains out of an existing domains, forest is a collection of trees. interconnected trees need to have a trust-policy (which can be either one-way or two-way trust)

![5 Common Mistakes in AD Recovery and How to Avoid Them | Fidelis Security](https://fidelissecurity.com/wp-content/uploads/2024/05/Active-Directory-Structure.webp align="left")

## Setting up a Local lab

You might need a specification of at least 16GBs of RAM and at least 256 GBs of SSD storage, if not possible locally, consider a Cloud-based setup on Azure/AWS

Here’s what you’ll need:

1. Windows server 2019
    
2. Least 2 Windows 10 enterprise edition
    
3. One Attackbox VM (like Kali/Parrot)
    

For Windows-based VMs, you can set aside 50-60GBs of disk space, and 25 GBs for the attackbox to enumerate and exploit your network. The server VM will act as the domain controller, while the enterprise VMs will act as client machines on the network. Please allocate at least 6 GBs of RAM to each and set the network type to NAT.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737381942641/b90a5505-9da5-4f04-b0f5-361bcd51fe92.png align="center")

Alright, let’s dive into authentication next!

## Organs of Kerberos

We have 4 prime parts in the protocol: the user primarily, the domain controller consisting of the authentication server + ticket granting server and finally the resource or service provider.

The authentication server ensures that an existing and valid user is requesting a service, the ticket granting server authenticates the request for the particular service to the user.

### Symmetric keys

Kerberos uses symmetric key cryptography is validate, encrypt and decrypt messages. Here’s a cool chart for what kind of algorithm is supported:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737443448803/7ef962d7-70ea-41b4-a493-acb85a0e03cf.png align="center")

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">Symmetric key cryptography is the process of using the same key to encrypt and decrypt a message</div>
</div>

### Caches and key tables

Users have their own unique user cache that stores the service ticket used to access the service.

Authentication service has a table to match user ids with their respective client secret keys. Similar case for the ticket granting service.

Meanwhile, the service only holds the service cache which stores the user authenticator message.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">user authenticator is a message that holds the user_id trying to access the resource.</div>
</div>

## Protocol workflow

![Image](https://media.discordapp.net/attachments/725059333871632416/1331131433917354147/image.png?ex=67908041&is=678f2ec1&hm=87e318ceafae3eb6db30d909d28cae737d11da5c6001345202af8f3105fb57c8&=&format=webp&quality=lossless&width=950&height=560 align="left")

The user sends a request for a “Ticket granting ticket” that can be sent to the TGS to get a service ticket. The auth service matches the user id with the respective client secret key (also ensuring if the user exists) and then sends back the TGT metadata encrypted with the client secret key and the TGT encrypted with the TGS secret key.

The user can only decode and check the acknowledgement from the TGT meta through the secret key generated by hashing the mentioned format in the diagram mentioned. (&lt;password&gt;&lt;user&gt;@something.com&lt;key version&gt;)

The user sends the user authenticator encrypted with the TGS session key from the TGT metadata, and the TGT which is still encrypted. The TGS now decrypts the TGT and checks the contents through the key stored in the TGS key table.

Now, the user receives the service metadata encrypted with TGS session key (which has a temporary fixed lifetime) along with the service ticket encrypted with a service secret key. Once again, the user can’t view the contents of the service ticket. The TGS session key now is used to help decrypt and acknowledge the service metadata. Finally, the service ticket is sent to the resource along with an User authenticator message encrypted with service session key received from the service meta-data.

Ultimately, we receive the service authentication and finally decrypt it through the service session key. And now we can use the service.