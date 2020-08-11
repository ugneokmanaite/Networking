
![image](https://github.com/ugneokmanaite/Networking/blob/master/images/networking.png)


## What is a network?
- 2 or more computers that are linked in order to share resources, exchange files, or allow electronic communications
- Local Area Network (LAN): network which is confined in relatively small area & limited to a geographic area e.g. building. 
- Wide Area Network (WAN): connect networks in larger georgraphcal areas e.g. UK or the World. Dedicated transoceanic cabling or satellite uplinks may be used

![image](https://cdn.techterms.com/img/lg/network_95.png)

## What is an IP?
- Internet Protocol Address
- 'Address'part refers to a unique number thar gets linked to online activity you do
- First you connect to a network that is connected to the internet and gives you access to the internet
- That network may be home internet provided, wireless network at hotel etc
- 2 standards of IP addresses: IPv4 and IPv6

- IPv4 uses 32 binary bits to create a single unique address on network. Expressed by 4 numbers separated by dots e.g. `216.27.61.137`

- IPv6 uses 128 binary bits to create a single uniue address on network. Expressed by eight grops of hexadeical numbers separeted by colons e.g. ` 0000:00000:0000:0000:3257:9531`

- IP address can be dynamic or static 
- While computers read IP addresses as binary code (a series of 1s and 0s), IP addresses are usually written as a series of alphanumeric characters.

## IPV4 vs IPV6

![image](https://bluecatnetworks.com/wp-content/uploads/2019/11/ipv4-ipv6.jpg)

## What is a subnet?
- Also known as a subnetwork
- A network inside another network 
- Network traffic can travel a shorter distance without passing through unecessary routers to reach destination

![image](https://www.cloudflare.com/resources/images/slt3lc6tev37/2pBqIHUTSlxI7EW9XZPKf3/551ab3390ab9ab86fee15c73fd245f6c/subnet-diagram.svg)

## Network class
- IP address has 2 parts: 1st part indicate which network the address belongs to, 2nd specified the device within that network
- Class A: can connect million of devices. Everything before the first period indicates the network, and after specifies the device. E.g.

`203.0.113.112` = 203 i the network 

- Class B: Everything before second period indicates the network.

- Class C: Everything before the third period indicates the network

## Subnet masks
- Like a IP addres but only for internal usage within a network
- IP address is divided into 2 parts: network & host
 - e.g. Class A = 8 network bits and 24 hots bits = this is because te default subnet mask for classA IP is 8 bit or 25.0.0.0 (decimal notation)
![image](https://github.com/ugneokmanaite/Networking/blob/master/images/submask.JPG)

## CIDR Blocks
- Classless Inter-Domain Routing
- Alternative to traditional subnetting
- You can add a speficication int he IP adddress itself as to the number of significant bits that make up the routing or network portion 
- [click here for more info](https://www.digitalocean.com/community/tutorials/understanding-ip-addresses-subnets-and-cidr-notation-for-networking)

##  What is inside a common 2 tier vpc? 

## N-tier
- Division of system into logical tiers 
- This is usually done with networking
- It alows us to build some robustness, flexibility & security 


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

Summary 
- create 2 subnets: public & private 

- none of them will have internet until we create something known as internet gateway

- the route table will have a public(which will include the application) and private route (which will include the database)

- what will happen is that internet will travel into route table

- final objective is for us to deploy our app 

- We will have security around the public subnet and the app & around the private subnet and DB

- public & private will be able to communicate with each other via the route table

1. We need an IP for VPC
2. We need IP for public subnet
3. We need UP for private subnet


## Step 1: Sign into Amazon Web Services
- Services --> VPC
- Choose Ireland location
- When choosing the area be aware it's not the same as availability zones
- Region = close cluster of data cantres
- Availability zones = within region= logically connected but physically segregated data centres inside a Region

## Step 2 : Create VPC
Your VPC- Create VPC
![image](https://github.com/ugneokmanaite/Networking/blob/master/images/create_vpc.JPG)

## Step 3: Create internet gateway
- > Internet gateway
- > Create 
- > Give name 

## Step 4: Attach internet gateway to VPC
- select the one just made
![image](https://github.com/ugneokmanaite/Networking/blob/master/images/attach%20internet%20gateway.JPG)

## Step 5: Create subnets
- > on the left menu go on subnets
- > create subnet

Creating public subnet
![image](https://github.com/ugneokmanaite/Networking/blob/master/images/Creating%20public%20subnet.JPG)

Creating private subnet
![image](https://github.com/ugneokmanaite/Networking/blob/master/images/private%20subnet.JPG)

## Step 6: Create routes
- >Route table option from menu on the left
- > there is a default already in there
![image](https://github.com/ugneokmanaite/Networking/blob/master/images/all%20routes%20displayed.JPG)

Add new one 
![image](https://github.com/ugneokmanaite/Networking/blob/master/images/adding%20route%20table.JPG)

- once created edit routes
- add 0.0.0.0/0


## Step 7 : Edit subnet associations
- click on public and save

(existing one gets automaticall associated to the main)


## Step: 7: Build some security
 
### Rules public

Ingress rules
- Allow port 80- for internet
- Allow port 443 
- Allow port 22 on range of IPs
- Allow Ephemeral ports

Egress rules
- Allow all

### Rules for private
Ingress Rules

- Only allow inbound traffic from public subnet
- 27017 from (IP address chosen for private)

Egress rules
- Allow all to (chosen priate IP 


## Step 8: Create Another ACL
- > Create network button
- > Add name and VPC just made
- > Inbound and outbound rules are now deny all and has no subnet associations.

## Step 9: Edit inbound rules

![image](https://github.com/ugneokmanaite/Networking/blob/master/images/edit%20inbound%20rules.JPG)

- rule #140 is bottom is my home IP and below is database IP

## Step 10: Edit outbound rules
![image](https://github.com/ugneokmanaite/Networking/blob/master/images/edit%20inbound%20rules.JPG)


## Step 11: Insert this security into my subnet

- > network ACLs
- > edit subnet associations & allow public


Now refresh and go on instances 

## Step 12: Launch instance
- use our network just created 
![image](https://github.com/ugneokmanaite/Networking/blob/master/images/new%20instance.JPG)

add tags
![image](https://github.com/ugneokmanaite/Networking/blob/master/images/add%20tags.JPG
)

select key pair
![image](https://github.com/ugneokmanaite/Networking/blob/master/images/key%20pair.JPG)

## Step 13: ssh into the system on bash terminal 

in terminal sudo apt-get install nginx
![image](https://github.com/ugneokmanaite/Networking/blob/master/images/ssh%20in.JPG)

check the browser with the IP address from instance just created

![image](https://github.com/ugneokmanaite/Networking/blob/master/images/welcome%20to%20nginx.JPG)