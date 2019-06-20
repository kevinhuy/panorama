# Configure Security Policies Panorama

This playbook takes a .xlsx file as input to configure network objects, service objects and security polcies on Panorama.  

# Pre-requisites

1. [requirements.txt](https://gitlab.com/Sudarshan_K/panorama/raw/master/requirements.txt) has all the libraries that need to be installed  
    ```
    pip install -r requirements.txt
    ```
2. Requires you to install the Paloaltonetworks Galazy Role
=======
1. [requirements.txt](https://gitlab.com/Sudarshan_K/panorama/raw/master/requirements.txt) has all the libraries that need to be installed.  
2. Requires you to install the Paloaltonetworks galaxy role
    ```
    ansible-galaxy install PaloAltoNetworks.paloaltonetworks,v2.0.4 --force
    ```
3. [xls_to_facts.py](https://raw.githubusercontent.com/mamullen13316/ansible_xls_to_facts/master/xls_to_facts.py) needs to be copied onto ansible/module/files/ as this module is not shipped with ansible.  
4. update panos_security_rule.py in galaxy roles to [this](https://raw.githubusercontent.com/PaloAltoNetworks/ansible-pan/f7cf604ab3c9c6eb2cab8f4fcc1653cb67251cee/library/panos_security_rule.py). Use the following command to find the location of file in your environment.   
    ```
    ansible-galaxy info PaloAltoNetworks.paloaltonetworks | grep path
    ```

# Files

[secrets.yaml](https://gitlab.com/Sudarshan_K/panorama/raw/master/secrets.yaml) contains the ip address of the panorama and the login credientials.  
[attributes.yaml](https://gitlab.com/Sudarshan_K/panorama/raw/master/attributes.yaml) contains security policy attributes  like the security profile, position, rule type and log settings.    
[configuration.xlsx](https://gitlab.com/Sudarshan_K/panorama/blob/master/variables/configuration.xlsx) is the input file with the policy information.    

### Input file [configuration.xlsx](https://gitlab.com/Sudarshan_K/panorama/blob/master/variables/configuration.xlsx)
Below are formats to follow when populating the input file.
1. Filename, Sheetnames and column names **can not** change.
2. FirewallPolicies Sheet - SourceZone, SourceIP, DestinationZone, DestinationIP, Application and Services can be either a list or a single value eg:- tcp_444, tcp_555 or tcp_444
3. NetworkObjects Sheet - Objects can be a list or a single value but needs to be in single quotes (') eg:- 'member1','member2' or 'member1'


# Executing the playbook

The playbook can be executed by executing the below command in a terminal.
```
ansible-playbook /path/to/file/configure.yaml
```

# Author

Sudarshan Vijaya Kumar

---

##### useful excel formulas for Network Object Groups
=IF(ISBLANK(B2),"",CONCAT("'",B2,"'"))  
=TEXTJOIN(",",TRUE,G2:K2)