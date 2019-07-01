# Configure Security Policies Panorama

This playbook takes a .xlsx file as input to configure network objects, service objects and security polcies on Panorama.  

# Pre-requisites

1. [requirements.txt](https://gitlab.com/Sudarshan_K/panorama/raw/master/requirements.txt) has all the libraries that need to be installed. 
    ```
    pip install -r requirements.txt
    ```
2. Requires you to install the Paloaltonetworks galaxy role
    ```
    ansible-galaxy install PaloAltoNetworks.paloaltonetworks,v2.2.2 --force
    ```
3. [xls_to_facts.py](https://raw.githubusercontent.com/mamullen13316/ansible_xls_to_facts/master/xls_to_facts.py) needs to be copied onto ansible/module/files/ as this module is not shipped with ansible.
    

# Files

[secrets.yaml](https://gitlab.com/Sudarshan_K/panorama/raw/master/secrets.yaml) contains the **ip address** of the panorama, the **login credientials** and the **source file** name.   

### Source file - Needs to be in the variables folder 

Have a look at a sample source file [here](https://gitlab.com/Sudarshan_K/panorama/blob/master/variables/sample-sourcefile.xlsx)

Below are formats to follow when populating the input file.
1. Filename, Sheetnames and column names **can-not** change.
2. NetworkObjects - Defined the Network Objects.
3. NetworkGroup Sheet - Defines the Network Objects. Objects can be a list or a single value but needs to be in single quotes (') eg:- 'member1','member2' or 'member1'
4. Services - Defines the Service Objects that need to be configured
5. ServiceGroups - Defines the Service Group Objects that need to be configured
6. FirewallPolicies - Defines the security policies that are to be configured.

# Playbooks
Execute the Playbook in the below order to ensure all dependencies are met to configure Security Policies.

##### panos-check.yaml
Checks the connection of the script server to Panorama instance, executed by command
```
ansible-playbook /path/to/file/panos-check.yaml
```

##### configure-network-objects.yaml
Configures the Network objects and Network Group Objects, executed by command  
```
ansible-playbook /path/to/file/configure-network-objects.yaml
```
Execution logs are written to logs/networkaddresses-log.csv and logs/networkobjects-log.csv

##### configure-service-objects.yaml
Configures the Service objects and Service Group Objects, executed by command  
```
ansible-playbook /path/to/file/configure-service-objects.yaml
```
Execution logs are written to logs/serviceobjects-log.csv and logs/servicegroups-log.csv

##### configure-security-policy.yaml
Configured the security-policy.yaml, executed by command  
```
ansible-playbook /path/to/file/configure-security-policy.yaml
```
Execution logs are written to logs/securitypolicy.csv


### Author
Sudarshan Vijaya Kumar

---

##### useful excel formulas for Network Object Groups
=IF(ISBLANK(B2),"",CONCAT("'",B2,"'"))  
=TEXTJOIN(",",TRUE,G2:K2)