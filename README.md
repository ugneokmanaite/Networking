
![image](https://github.com/ugneokmanaite/Networking/blob/master/images/networking.png)


## What is a network?
- 2 or more computers that are linked in order to share resources, exchange files, or allow electronic communications
- Local Area Network (LAN): network which is confined in relatively small area & limited to a geographic area e.g. building. 
- Wide Area Network (WAN): connect networks in larger georgraphcal areas e.g. UK or the World. Dedicated transoceanic cabling or satellite uplinks may be used

![image](https://www.google.com/url?sa=i&url=https%3A%2F%2Ftechterms.com%2Fdefinition%2Fnetwork&psig=AOvVaw2kJyJOUderi3DpdyEAxdRA&ust=1597237369331000&source=images&cd=vfe&ved=0CAIQjRxqFwoTCMjjrIKbk-sCFQAAAAAdAAAAABAK)

## What is an IP?
- Internet Protocol Address
- 'Address'part refers to a unique number thar gets linked to online activity you do
- First you connect to a network that is connected to the internet and gives you access to the internet
- That network may be home internet provided, wireless network at hotel etc
- 2 standards of IP addresses: IPv4 and IPv6.
- IPv4 uses 32 binary bits to create a single unique address on network. Expressed by 4 numbers separated by dots e.g. `216.27.61.137`

- IPv6 uses 128 binary bits to create a single uniue address on network. Expressed by eight grops of hexadeical numbers separeted by colons e.g. ` 0000:00000:0000:0000:3257:9531`

- IP address can be dynamic or static 
- While computers read IP addresses as binary code (a series of 1s and 0s), IP addresses are usually written as a series of alphanumeric characters.

## Maximum IP in IPV4?

## IPV4 vs IPV6

![image](https://bluecatnetworks.com/wp-content/uploads/2019/11/ipv4-ipv6.jpg)

## What is a subnet?
- Also known as a subnetwork
- A network inside another network 
- Network traffic can travel a shorter distance without passing through unecessary routers to reach destination

![image](https://www.cloudflare.com/resources/images/slt3lc6tev37/2pBqIHUTSlxI7EW9XZPKf3/551ab3390ab9ab86fee15c73fd245f6c/subnet-diagram.svg)

## Netork class
- IP address has 2 parts: 1st part indicate which network the address belongs to, 2nd specified the device within that network
- Class A: can connect million of devices. Everything before the first period indicates the network, and after specifies the device. E.g.

`203.0.113.112` = 203 i the network 

- Class B: Everything before second period indicates the network.

- Class C: Everything before the third period indicates the network

## Subnet masks
- Like a IP addres but only for internal usage within a network
- 

## CIDR Blocks

##  What is inside a common 2 tier vpc? 

## N-tier
- Division of system into logical tiers 
- This is usually done with networking
- It alows us to build some robustness, flexibility & security 
-


## VPC 
- IGW
- Subnet
- NACLs
- Route Tables
- SG 
- EC2

Objective :
- [x] Create a classical tier architecture VPC for our web app and DV
- [x] It will have a public subnet and private subnet
- [x] The above is N-tier practice
- [x] Getting it to work and communications & setting up all of the networing  will be the netowrk practice

## VPC
- Virtual private cloud in AWS to launch computing resources 

## IGW
- Internet Gateway
- Attached to the VPC 
- Allows internet into VPC via route table

## Subnets 
- Internal Networking

## NACLs
- Network Access Control lists 
- It's a firewall at the level of the subnet

## Route Tables 
- Contains set of rules known as routes that are used to determine where network traffic from your subnet or gateway is directed

## EC2
- Elastic compute cloud 
- It is a VM machine on cloud

## Security group
- It is a firewall - at the level of EC2 (instance)

Acceptance Criteria
- [x] has a private sub
- [x] has a public sub
- [x] is your own vpc
- [x] public sub has internet access
- [x] has the right routes 
- [x] app exists in public sub
- [x] DB exists in private sub
- [x] Networking is done correctly 


- create 2 subnets: public & private 

-none of them will have internet until we create something known as internet gateway

- the route table will have a public(which will include the application) and private route (which will include the database)

- what will happen is that internet will travel into route table

- final objective is for us to deploy our app 

- We will have security around the public subnet and the app & around the private subnet and DB

- public & private will be able to communicate with each other via the route table

1. We need an IP for VPC
2. We need IP for public subnet
3. We need UP for private subnet


1. Sign in into Amazon Web Services

2. Services- VPC

3. When choosing the area be aware it's not the same as availability zones

region = close cluster of data cantres

availability zones = within region= logically connected but physically segregated data centres inside a Region

4. Your VPC- Create VPC
![image]()

5. Now create internet gateway
- internet gateway
- create 
- give name 

6. Attach internet gateway to VPC & select the one just made
![image]()

7. Create subnets!
- on left go on subnets
- create subnet

Creating public subnet
![image]()

Creating private subnet
![image]()

8. Now we need to create routes
- Route table on left
- there is a default already in there (add pic)

(addnew one)
- once created edit routes
- add 0.0.0.0/0

- edit subnet associations - click on public and save

(other one gets automaticall associated to the main)

now go back to VPC - we need to build some security

key thing is that in ec2 instances  

outbound rules = by default everyone is allowed out 

INGRESS= ssh for us and automation servers(jenkins), dev port for us and internet ports for the world

EGRESS = Default 0.0.0.0/0

now we need to build these rules for the subnets

NACLs 
- require outbound rules to set and by default deny all outbound traffic
- rules numbers matter
- you can deny any IP as well as allow 

### Rules public

Ingress rules
- Allow port 80- for internet
- Allow port 443 
- Allow port 22 on range of IPs
- Allow Ephemeral ports

Egress rules
- Allow all

### Rules for private
- Only allow inbound traffic from public subnet
- 27017 from (IP address chosen for private)

Egress
- Allow all to (chosen priate IP 


Create Anoter ACL
Create network button - add name and VPC just made

inbound and outbound rules are now deny all and has no subnet associations.

- edit inbound rules

![image]()

- bottom is my home IP and below is database IP

- edit outbound rules
![image]()

- Now i need to insert this security into my subnet

- network ACLs- edit subnet associations & allow public

No refresh and go on instances - launch instance- use our network just created 
![image]()

add tags
select key pair
ssh into the system on bash terminal 