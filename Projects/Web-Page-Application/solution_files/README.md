## SOLUTION STEPS

### Notes!!
- Let the "AmazonEC2FullAccess" role be assigned to the Control Instance
- Use your own .pem file in the key part of the files
- Don't forget to set the Paths in the file according to your own
- DB_HOST=<your_postresql_instance_private-ip> in nodejs/.env file
- REACT_APP_BASE_URL=<your_nodejs_instance_public-ip> in react/.env file


1. Enter the following command for dynamic inventory
```
 pip3 install --user boto3
```
2. Create `inventory_aws_ec2.yml`. You can see the relevant file in the ansible-project/nodejs folder.

3. Run the commands below and see the hosts

```
 ansible-inventory -i inventory_aws_ec2.yml --graph
```

4. Create a dockerfile for Nodejs, postgres and react. You can see the relevant file in the ansible-project/nodejs folder.

5. Create `docker_postgre.yml`. Available under ansible folder. Check paths!

6. Run docker_postgre.yml use Vault.
```
ansible-vault create secret.yml
```
```
ansible-playbook --ask-vault-pass docker_postgre.yml
```
```
ansible _ansible_postgresql -b -m shell -a "docker ps"
```
7. Create `docker_nodejs.yml`. Available under ansible folder. Check paths!

```
ansible-playbook docker_nodejs.yml
```
```
ansible _ansible_nodejs -b -m shell -a "docker ps"
```

8. Create `docker_reacts.yml`. Available under ansible folder. Check paths!

```
ansible-playbook docker_react.yml
```
```
ansible _ansible_react -b -m shell -a "docker ps"
```