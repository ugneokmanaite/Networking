## Step 1: Ensure the following have been configured:

1. VPC 
2. Internet Gateway (IGW)
3. Create subnets (public & private)
4. Create appropriate routes via route table
5. Create ACLs
6. Edit inbound & outbound rules to desired security level
7. Insert ACL security into subnets
8. Launch instance for APP, DB & Bastion

For VPC, IGQ, Subets, Route table, ACL [click here](https://github.com/ugneokmanaite/Networking)

For Bastion configuration [click here](https://github.com/ugneokmanaite/Networking/Bastion_Server)

## STEP 1: SSH Into App instance
- run the provision file
- `cd app`

- `npm install`

- `node app.js`

## STEP 2: SSH into Bastion instance 
- Keep the app running & open a new bash terminal

- 

## STEP 3: SSH into DB intance through Bastion VM
- run the db provision file
- check that the db is running

`sudo systemctl status mongod`





